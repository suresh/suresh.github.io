---
title: "Sagemaker Save data"
permalink: /snippets/sagemaker-save-s3/
excerpt: "How the theme is organized and what all of the files are for."
last_modified_at: 2018-03-20T15:19:22-04:00
---

# Sagemaker save Dataframe to S3 Bucket

After preparing a dataframe using feature engineering pipeline, it is good practice to write the file back to S3 store. You can use this code snippet to write file back: 

```python
filename = 'data/dataframe_20190809.csv'
DESTINATION = bucket

def _write_dataframe_to_csv_on_s3(dataframe, filename):
    """ Write a dataframe to a CSV on S3 """
    print("Writing {} records to {}".format(len(dataframe), filename))
    # Create buffer
    csv_buffer = StringIO()
    # Write dataframe to buffer
    dataframe.to_csv(csv_buffer, sep=",", index=False)
    # Create S3 object
    s3_resource = boto3.resource("s3")
    # Write buffer to S3 object
    s3_resource.Object(DESTINATION,filename).put(Body=csv_buffer.getvalue())

_write_dataframe_to_csv_on_s3(securities_metrics_data_groupby, filename)
```
