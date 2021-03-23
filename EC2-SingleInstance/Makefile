include .env

STACKNAME := aws-ec2-si-study-guide
BUCKET := aws-cf-b-study-templates
KEYFILE_ARG := ${KEYFILE}

STACK_CLI_ARGS := --template-url https://$(BUCKET).s3.amazonaws.com/EC2SingleInstance.yaml \
					--stack-name ${STACKNAME} \
					--parameters \
					ParameterKey=KeyName,ParameterValue=$(KEYFILE_ARG) \
					--capabilities CAPABILITY_IAM

all:
	aws cloudformation create-stack $(STACK_CLI_ARGS)

create_bucket:
	aws s3 mb s3://$(BUCKET)

fetch_bucket:
	aws s3 sync . s3://$(BUCKET) --exclude "Makefile" --exclude ".env"

clean_bucket:
	aws s3 rb s3://$(BUCKET) --force

delete_stack:
	aws cloudformation delete-stack --stack-name $(STACKNAME)