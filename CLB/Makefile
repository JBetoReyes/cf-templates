include .env

STACKNAME := aws-ec2-si-study-guide
BUCKET := aws-cf-b-study-templates
KEYFILE_ARG := ${KEYFILE}

STACK_CLI_ARGS := --template-url https://$(BUCKET).s3.amazonaws.com/master.yaml \
					--stack-name ${STACKNAME} \
					--parameters \
					ParameterKey=KeyName,ParameterValue=$(KEYFILE_ARG) \
					ParameterKey=LBAvailabilityZone1,ParameterValue=$(AVAILABILITY_ZONE1) \
					ParameterKey=LBAvailabilityZone2,ParameterValue=$(AVAILABILITY_ZONE2) \
					--capabilities CAPABILITY_IAM

all: sync_bucket
	aws cloudformation create-stack $(STACK_CLI_ARGS)

create_bucket:
	aws s3 mb s3://$(BUCKET)

update_stack: sync_bucket
	aws cloudformation update-stack $(STACK_CLI_ARGS)

sync_bucket:
	aws s3 sync . s3://$(BUCKET) --exclude "Makefile" --exclude ".env"

clean_bucket:
	aws s3 rb s3://$(BUCKET) --force

delete_stack:
	aws cloudformation delete-stack --stack-name $(STACKNAME)