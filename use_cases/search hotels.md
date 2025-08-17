## 📖 Documentation: Hotel Search & Filter (Guest Users)

### Overview 
The **Hotel Search & Filter** module allows guest users to search for hotels in a destination city, apply filters (price, rating, amenities, etc.), and view available results. The system integrates with the Amadeus API for real-time hotel availability and pricing.



### Actors

- Guest User: Unauthenticated users browsing/searching hotels.
- Amadeus API: External service providing hotel data (availability, pricing, details, etc.). 



### Constraints
- Guest users can search and filter without logging in.

- Filters apply only to the results fetched from Amadeus API.

- Rate limits and API quotas of Amadeus must be respected.

- Network latency may affect response time (optimize with caching where possible).

- Data freshness depends on Amadeus responses.


### Sequence Diagram
![sequence diagram](https://drive.google.com/uc?export=view&id=1l91T5e6_FtTwCQUZDWj8nLi_ku5FkPIz)



### Flow Diagram
![flow diagram](https://drive.google.com/uc?export=view&id=1t5ZFGDA6d2c3tR5t4amradZc_2ytHxAO)



### Use Cases 

#### UC1: Search Hotels

**Description**: Guest user searches for hotels in a given city for specified dates.

**Actors**: Guest User, System, Amadeus API.

**Pre-condition**: User is on the hotel search page.

**Post-condition**: User sees a list of hotels.

**Main Flow**:

1. Guest enters:

    - Destination (city/airport code).
    - Check-in & check-out dates.
    - Number of guests/rooms.

2. System validates input.

3. System sends request to Amadeus API */v2/shopping/hotel-offers*.

4. Amadeus returns available hotels.

5. System formats results and displays to the user.

**Alternative Flows**:

- Invalid input → show error.

- API failure → show fallback message.

--- 

#### UC2: Filter Hotels

**Description**: Guest applies filters on search results.

**Actors**: Guest User, System.

**Pre-condition**: 

**Post-condition**: User sees a filtered list.

**Filters**:

- Price range
- Star rating
- Amenities (Wi-Fi, pool, parking, etc.)
- Distance from city center
- Hotel chains

**Main Flow**:

1. Guest selects filter criteria.

2. System applies filters to hotel list (either client-side or server-side).

3. Filtered results are displayed.

---

### API Design

**Endpoint**: GET /api/hotels/search

**Description**: Search hotels using Amadeus API.

**Request Parameters**:
```json
{
  "cityCode": "CAI",
  "checkInDate": "2025-09-01",
  "checkOutDate": "2025-09-05",
  "adults": 2,
  "roomQuantity": 1,
  "currency": "USD"
}
```

**Response Example:**:
```json
{
  "data": [
    {
      "hotelId": "H1234",
      "name": "Hilton Cairo",
      "rating": 5,
      "price": {
        "total": "450.00",
        "currency": "USD"
      },
      "amenities": ["wifi", "pool", "parking"],
      "distance": 2.5
    }
  ]
}
```

---

**Endpoint**: POST /api/hotels/filter

**Description**: Filter hotels after search.

**Request Parameters**:
```json
{ 
  "filters": {
    "priceMin": 100,
    "priceMax": 500,
    "rating": [4, 5],
    "amenities": ["wifi", "pool"]
  }
}
```

**Response Example:**:
```json
{
  "filteredHotels": [
    {
      "hotelId": "H1234",
      "name": "Hilton Cairo",
      "rating": 5,
      "price": {
        "total": "450.00",
        "currency": "USD"
      },
      "amenities": ["wifi", "pool", "parking"]
    }
  ]
}
```
---

### Pseudo Code

```typescript
function searchHotels(cityCode, checkInDate, checkOutDate, adults, roomQuantity) {
    // Validate inputs
    if (!cityCode || !checkInDate || !checkOutDate) {
        throw new Error("Invalid search parameters");
    }

    // Call Amadeus API
    const response = amadeusAPI.get("/v2/shopping/hotel-offers", {
        cityCode, checkInDate, checkOutDate, adults, roomQuantity
    });

    // Format results
    return response.data.map(hotel => ({
        id: hotel.hotel.hotelId,
        name: hotel.hotel.name,
        rating: hotel.hotel.rating,
        price: hotel.offers[0].price.total,
        amenities: hotel.hotel.amenities,
        distance: hotel.hotel.distance?.value
    }));
}

function filterHotels(hotels, filters) {
    return hotels.filter(hotel => {
        return hotel.price >= filters.priceMin &&
               hotel.price <= filters.priceMax &&
               filters.rating.includes(hotel.rating) &&
               filters.amenities.every(a => hotel.amenities.includes(a));
    });
}
```



