**API Documentation**

### 1. Check if a Vehicle is Currently in the Parking Lot  
**Endpoint**  
`GET /parking/status/:carPlate`  

**Description**  
This endpoint checks whether a vehicle with the specified license plate is currently in the parking lot.  

**Parameters**  
| Parameter | Type | Required | Description |  
|-----------|------|----------|-------------|  
| `carPlate` | string | Yes | The license plate to query, provided as a URL path parameter. |  

**Example Request**  
```http  
GET /parking/status/ABC-123  
```  

**Response**  
| Field | Type | Description |  
|-----------|------|-------------|  
| `carPlate` | string | The queried license plate. |  
| `isInLot` | boolean | Indicates if the vehicle is in the parking lot (`true` = present, `false` = not present). |  

**Example Response**  
```json  
{  
  "carPlate": "ABC-123",  
  "isInLot": true  
}  
```  

---

### 2. Check Current Vehicle Count in the Parking Lot  
**Endpoint**  
`GET /parking/count`  

**Description**  
This endpoint retrieves the current number of vehicles in the parking lot.  

**Parameters**  
None.  

**Example Request**  
```http  
GET /parking/count  
```  

**Response**  
| Field | Type | Description |  
|-------|------|-------------|  
| `count` | number | Current vehicle count in the parking lot. |  

**Example Response**  
```json  
{  
  "count": 5  
}  
```  

---

### WebSocket API Documentation  
**Endpoint**  
`ws://localhost:3000`  

**Description**  
The WebSocket interface provides real-time updates about vehicles entering or being denied entry to the parking lot. After connecting, the server periodically pushes simulated vehicle event messages.  

#### Message Formats  

**1. Vehicle Entry**  
Sent when a vehicle enters the parking lot.  

| Field | Type | Description |  
|-----------|------|-------------|  
| `type` | string | Message type: `enter`. |  
| `carPlate` | string | License plate of the entering vehicle. |  

**Example Message**  
```json  
{  
  "type": "enter",  
  "carPlate": "ABC-123"  
}  
```  

**2. Parking Lot Full**  
Sent when the parking lot is full and cannot accommodate more vehicles.  

| Field | Type | Description |  
|-----------|------|-------------|  
| `type` | string | Message type: `full`. |  
| `carPlate` | string | License plate of the vehicle denied entry. |  

**Example Message**  
```json  
{  
  "type": "full",  
  "carPlate": "ABC-456"  
}  
```  
