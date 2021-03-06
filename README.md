## PTV API Node client

This is a simple client library for the PTV API, using their(*) published Open API definition at https://timetableapi.ptv.vic.gov.au/swagger/ui/index. It supports version 3 of the API.

It is really just the Swagger-Client library, with a convenience method to automatically add your devid and calculate the required signature.

### Usage

`npm install ptv-api`

```
const ptv = require('ptv-api');

const devid = '2';
const apikey = '12345-eat-faded-g00-907852341';

ptvClient = ptv(devid, apikey); 
ptvClient.then(apis => {
    return apis.Routes.Routes_RouteFromId({ route_id: 8960 });
}).then(res => {
    console.log(res.body);
}).catch(console.error);
```

This prints:

```
{ route:
   { route_type: 4,
     route_id: 8960,
     route_name: 'Night Bus - City - Collingwood - Eastern Fwy - Templestowe - Doncaster',
     route_number: '961',
     route_gtfs_id: '8-961' },
  status: { version: '3.0', health: 1 } }
```

### API

These methods are exposed:

```
Departures.Departures_GetForStop
Departures.Departures_GetForStopAndRoute
Directions.Directions_ForRoute
Directions.Directions_ForDirection
Directions.Directions_ForDirectionAndType
Disruptions.Disruptions_GetAllDisruptions
Disruptions.Disruptions_GetDisruptionsByRoute
Disruptions.Disruptions_GetDisruptionById
Patterns.Patterns_GetPatternByRun
RouteTypes.RouteTypes_GetRouteTypes
Routes.Routes_OneOrMoreRoutes
Routes.Routes_RouteFromId
Runs.Runs_ForRoute
Runs.Runs_ForRouteAndRouteType
Runs.Runs_ForRun
Runs.Runs_ForRunAndRouteType
Search.Search_Search
Stops.Stops_StopsByGeolocation
Stops.Stops_StopsForRoute
Stops.Stops_StopDetails
```

### Credits

Original OpenAPI (Swagger) spec by Steve Bennett. Updated and maintained by Public Transport Victoria. More information about using the API at https://www.ptv.vic.gov.au/about-ptv/data-and-reports/datasets/ptv-timetable-api/ .