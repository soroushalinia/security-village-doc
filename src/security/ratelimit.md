# Rate Limit

Rate limit is also applied to each route. The rate is also calculated for both ip
and user agent values and is atomic. This means that they are shared across workers.
Redis is also used as ratelimit backend.

Depeding on the estimated use case of each route, its rate limit will differ.
It could be as low as 5 request/minute for POST methods to maximum of 20 requests/minute
for GET methods in a route.