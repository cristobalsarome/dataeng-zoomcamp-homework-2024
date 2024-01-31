## Module 1 Homework

## Docker & SQL

In this homework we'll prepare the environment 
and practice with Docker and SQL


## Question 1. Knowing docker tags

Run the command to get information on Docker 

```docker --help```

Now run the command to get help on the "docker build" command:

```docker build --help```

Do the same for "docker run".

Which tag has the following text? - *Automatically remove the container when it exits* 

- `--delete`
- `--rc`
- `--rmc`
-  **`--rm`** ✅



## Question 2. Understanding docker first run 

Run docker with the python:3.9 image in an interactive mode and the entrypoint of bash.
Now check the python modules that are installed ( use ```pip list``` ). 

```
$ winpty docker run -it --entrypoint=bash python:3.9
root@991a1ab5030b:/# pip list
Package    Version
---------- -------
pip        23.0.1
setuptools 58.1.0
wheel      0.42.0
```

What is version of the package *wheel* ?

- **0.42.0** ✅
- 1.0.0
- 23.0.1
- 58.1.0


# Prepare Postgres

Run Postgres and load data as shown in the videos
We'll use the green taxi trips from September 2019:

```wget https://github.com/DataTalksClub/nyc-tlc-data/releases/download/green/green_tripdata_2019-09.csv.gz```

You will also need the dataset with zones:

```wget https://s3.amazonaws.com/nyc-tlc/misc/taxi+_zone_lookup.csv```

Download this data and put it into Postgres (with jupyter notebooks or with a pipeline)


## Question 3. Count records 

How many taxi trips were totally made on September 18th 2019?

Tip: started and finished on 2019-09-18. 

Remember that `lpep_pickup_datetime` and `lpep_dropoff_datetime` columns are in the format timestamp (date and hour+min+sec) and not in date.

- 15767
- **15612** ✅
- 15859
- 89009

**See code here:** [link to code](questions_3_to_6.ipynb)



## Question 4. Largest trip for each day

Which was the pick up day with the largest trip distance
Use the pick up time for your calculations.

- 2019-09-18
- 2019-09-16
- **2019-09-26** ✅
- 2019-09-21

**See code here:** [link to code](questions_3_to_6.ipynb)

## Question 5. Three biggest pick up Boroughs

Consider lpep_pickup_datetime in '2019-09-18' and ignoring Borough has Unknown

Which were the 3 pick up Boroughs that had a sum of total_amount superior to 50000?
 
- **"Brooklyn" "Manhattan" "Queens"** ✅
- "Bronx" "Brooklyn" "Manhattan"
- "Bronx" "Manhattan" "Queens" 
- "Brooklyn" "Queens" "Staten Island"

**See code here:** [link to code](questions_3_to_6.ipynb)

## Question 6. Largest tip

For the passengers picked up in September 2019 in the zone name Astoria which was the drop off zone that had the largest tip?
We want the name of the zone, not the id.

Note: it's not a typo, it's `tip` , not `trip`

- Central Park
- Jamaica
- **JFK Airport** ✅
- Long Island City/Queens Plaza

**See code here:** [link to code](questions_3_to_6.ipynb)


## Terraform

In this section homework we'll prepare the environment by creating resources in GCP with Terraform.

In your VM on GCP/Laptop/GitHub Codespace install Terraform. 
Copy the files from the course repo
[here](https://github.com/DataTalksClub/data-engineering-zoomcamp/tree/main/01-docker-terraform/1_terraform_gcp/terraform) to your VM/Laptop/GitHub Codespace.

Modify the files as necessary to create a GCP Bucket and Big Query Dataset.


## Question 7. Creating Resources

After updating the main.tf and variable.tf files run:

```
terraform apply
```

Paste the output of this command into the homework submission form.


```PS C:\Users\crist\OneDrive\Learning\Data-Engineering\dataeng-zoomcamp-homework-2023\week-1\terraform> terraform apply
var.project
  Your GCP Project ID

  Enter a value: 759274576604

google_storage_bucket.data-lake-bucket: Refreshing state... [id=dtc_data_lake_dataeng-zoomcamp-376312]
google_bigquery_dataset.dataset: Refreshing state... [id=projects/dataeng-zoomcamp-376312/datasets/trips_data_all]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following
symbols:
  + create
-/+ destroy and then create replacement

Terraform will perform the following actions:

  # google_bigquery_dataset.dataset will be created
  + resource "google_bigquery_dataset" "dataset" {
      + creation_time              = (known after apply)
      + dataset_id                 = "trips_data_all"
      + delete_contents_on_destroy = false
      + etag                       = (known after apply)
      + id                         = (known after apply)
      + labels                     = (known after apply)
      + last_modified_time         = (known after apply)
      + location                   = "us-west1"
      + project                    = "759274576604"
      + self_link                  = (known after apply)

      + access {
          + domain         = (known after apply)
          + group_by_email = (known after apply)
          + role           = (known after apply)
          + special_group  = (known after apply)
          + user_by_email  = (known after apply)

          + dataset {
              + target_types = (known after apply)

              + dataset {
                  + dataset_id = (known after apply)
                  + project_id = (known after apply)
                }
            }

          + routine {
              + dataset_id = (known after apply)
              + project_id = (known after apply)
              + routine_id = (known after apply)
            }

          + view {
              + dataset_id = (known after apply)
              + project_id = (known after apply)
              + table_id   = (known after apply)
            }
        }
    }

  # google_storage_bucket.data-lake-bucket must be replaced
-/+ resource "google_storage_bucket" "data-lake-bucket" {
      - default_event_based_hold    = false -> null
      ~ id                          = "dtc_data_lake_dataeng-zoomcamp-376312" -> (known after apply)
      - labels                      = {} -> null
      ~ name                        = "dtc_data_lake_dataeng-zoomcamp-376312" -> "dtc_data_lake_759274576604" # forces replacement
      ~ project                     = "dataeng-zoomcamp-376312" -> (known after apply)
      ~ public_access_prevention    = "inherited" -> (known after apply)
      - requester_pays              = false -> null
      ~ self_link                   = "https://www.googleapis.com/storage/v1/b/dtc_data_lake_dataeng-zoomcamp-376312" -> (known after apply)
      ~ url                         = "gs://dtc_data_lake_dataeng-zoomcamp-376312" -> (known after apply)
        # (4 unchanged attributes hidden)

      ~ lifecycle_rule {

          - condition {
              - age                        = 30 -> null
              - days_since_custom_time     = 0 -> null
              - days_since_noncurrent_time = 0 -> null
              - matches_prefix             = [] -> null
              - matches_storage_class      = [] -> null
              - matches_suffix             = [] -> null
              - num_newer_versions         = 0 -> null
              - with_state                 = "ANY" -> null
            }
          + condition {
              + age                   = 30
              + matches_prefix        = []
              + matches_storage_class = []
              + matches_suffix        = []
              + with_state            = (known after apply)
            }

            # (1 unchanged block hidden)
        }

      + website {
          + main_page_suffix = (known after apply)
          + not_found_page   = (known after apply)
        }

        # (1 unchanged block hidden)
    }

Plan: 2 to add, 0 to change, 1 to destroy.
```


## Submitting the solutions

* Form for submitting: https://courses.datatalks.club/de-zoomcamp-2024/homework/hw01
* You can submit your homework multiple times. In this case, only the last submission will be used. 

Deadline: 29 January, 23:00 CET
