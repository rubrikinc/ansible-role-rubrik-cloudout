Ansible Role: Rubrik CloudOut
=========

Complete the AWS configuration process required for the Rubrik CloudOut features that enables the use of an S3 bucket for archiving.

Requirements
------------

The follow requirements were pulled from the various AWS Modules used in this role:

* boto
* boto3
* botocore
* python >= 2.6

Role Variables
--------------

**Required**

| Variable  |  Description |
|---|---|
| s3_bucket_name  | The name of the S3 bucket where Rubrik will store archived snapshots.  |
| aws_region | The specific AWS region where the configurations will occur. Please use the "region" options listed in the [AWS documentation](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.RegionsAndAvailabilityZones.html) as values. |

**Default (see `defaults/main.yml`)**

| Variable  |  Default | Description  |
|---|---|---|
| create_new_user  | true  | Flag to determine if a new user specific to CloudOut is created. If the flag is set to `false` the role will associate the new S3 Security Policy with the IAM provided in the `iam_user` variable. |
| iam_user  | rubrik-cloudout  | The name of the IAM User that will be associated with Rubrik CloudOut IAM Policy created during this process. If `create_new_user` is set to `false` this value needs to be updated to an IAM user that has already been created.|
| s3_security_policy_name  | rubrik_cloudout  | The name of the IAM Policy that has all required permissions for Rubrik CloudOut.|
| s3_security_policy_description  | Security policy used for Rubrik CloudOut.  | The description of the IAM Policy that has all required permissions for Rubrik CloudOut.|

**Dynamically Generated (`vars/main.yml`)**

| Variable  |  Description |
|---|---|
| s3_bucket_arn  | The dynamically generated ARN of the S3 bucket provided in the `s3_bucket_name` variable and used in the `s3_security_policy.json.j2` template.  |

**Output**

When `create_new_user` is set to the default value of `true` the new IAM users Access and Secret Key will be provided at the end of the Playbook. Please note that the Secret key will only be provided during the Playbook run where it is first created.


```python
ok: [localhost] => {
    "msg": "Access Key - AKIAQQD3AFGPKHCV8L9Q"
}
```

```python
ok: [localhost] => {
    "msg": "Secret Key - 5a3E4bCIc87CpQQDimkNdIi4ree2CiASDFh1Uh8H"
}
```



Dependencies
------------

n/a

Example Playbook
----------------

    - hosts: localhost
      gather_facts: false
      roles:
        - rubrik-devops.rubrik-cloudout
      vars:
        s3_bucket_name: "example-bucket"
        aws_region: us-east-2

License
-------

GPLv3

Author Information
------------------

<p></p>
<p align="center">
  <img src="https://user-images.githubusercontent.com/8610203/37415009-6f9cf416-2778-11e8-8b56-052a8e41c3c8.png" alt="Rubrik Ranger Logo"/>
</p>
