include .env

STACKNAME := aws-rds-study-guide
BUCKET := aws-cf-b-study-templates
KEYFILE_ARG := ${KEYFILE}

STACK_CLI_ARGS := --template-url https://$(BUCKET).s3.amazonaws.com/master.yaml \
                                  --stack-name ${STACKNAME}  \
				  --parameters \
				  ParameterKey=KeyName,ParameterValue=$(KEYFILE_ARG) \
				  ParameterKey=AvailabilityZone1,ParameterValue=$(AVAILABILITY_ZONE1) \
				  ParameterKey=AvailabilityZone2,ParameterValue=$(AVAILABILITY_ZONE2) \
				  ParameterKey=DBName,ParameterValue=$(DB_NAME) \
				  ParameterKey=DBUser,ParameterValue=$(DB_USER) \
				  ParameterKey=DBPassword,ParameterValue=$(DB_PASSWORD) \
				  --capabilities CAPABILITY_IAM \
				  --capabilities CAPABILITY_NAMED_IAM
		
all: fetch_bucket
	aws cloudformation create-stack $(STACK_CLI_ARGS)

create_bucket:
	aws s3 mb s3://$(BUCKET)

update_stack: fetch_bucket
	aws cloudformation update-stack $(STACK_CLI_ARGS)

fetch_bucket:
	aws s3 sync . s3://$(BUCKET) --exclude "Makefile" --exclude ".env"

clean_bucket:
	aws s3 rb s3://$(BUCKET) --force

delete_stack:
	aws cloudformation delete-stack --stack-name $(STACKNAME)