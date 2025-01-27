
-> Question 1. Answer
    ![alt text](image.png)


-> Question 2. Understanding Docker networking and docker-compose

answer:
    db:5432

-> Question 3. Trip Segmentation Count

answer:
    104,802; 198,924; 109,603; 27,678; 35,189


    1. Up to 1 mile

        SELECT 
            count(*) 
        FROM public.green_tripdata
        where cast(lpep_pickup_datetime as date) between '2019-10-01' and '2019-10-31'
        and cast(lpep_dropoff_datetime as date) < '2019-11-01'
        and trip_distance <= 1


    2. In between 1 (exclusive) and 3 miles (inclusive)

        SELECT 
            count(*) 
        FROM public.green_tripdata
        where cast(lpep_pickup_datetime as date) between '2019-10-01' and '2019-10-31'
        and cast(lpep_dropoff_datetime as date) < '2019-11-01'
        and trip_distance <= 3 
        and trip_distance > 1

    3. In between 3 (exclusive) and 7 miles (inclusive)

        SELECT 
            count(*) 
        FROM public.green_tripdata
        where cast(lpep_pickup_datetime as date) between '2019-10-01' and '2019-10-31'
        and cast(lpep_dropoff_datetime as date) < '2019-11-01'
        and trip_distance <= 7 
        and trip_distance > 3

    4. In between 7 (exclusive) and 10 miles (inclusive)

        SELECT 
            count(*) 
        FROM public.green_tripdata
        where cast(lpep_pickup_datetime as date) between '2019-10-01' and '2019-10-31'
        and cast(lpep_dropoff_datetime as date) < '2019-11-01'
        and trip_distance <= 10 
        and trip_distance > 7

    5. over 10:

        SELECT 
            count(*) 
        FROM public.green_tripdata
        where cast(lpep_pickup_datetime as date) between '2019-10-01' and '2019-10-31'
        and cast(lpep_dropoff_datetime as date) < '2019-11-01'
        and trip_distance > 10

-> Question 4. Longest trip for each day

answer:
    2019-10-31

    SELECT 
        *
    FROM public.green_tripdata
    order by trip_distance desc


-> Question 5. Three biggest pickup zones

answer: 

    East Harlem North, East Harlem South, Morningside Heights

    SELECT 
        "Zone"
        ,sum(total_amount) as total_amount
    FROM public.green_tripdata gt
    left join zones z on gt."PULocationID" = z."LocationID"
    where cast(lpep_pickup_datetime as date) = '2019-10-18'
    group by "Zone"
    order by total_amount desc



-> Question 6. Largest tip

answer:

    JFK Airport

    SELECT 
        "Zone"
        ,tip_amount
    FROM public.green_tripdata gt
    left join zones z on gt."DOLocationID" = z."LocationID"
    where cast(lpep_pickup_datetime as date) between '2019-10-01' and '2019-10-31'
        and "PULocationID" = 74
    order by tip_amount desc