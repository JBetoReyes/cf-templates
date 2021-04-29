include .env

STACKNAME := aws-eks-study-guide
BUCKET := aws-cf-b-study-templates
KEYFILE_ARG := ${KEYFILE}

STACK_CLI_ARGS := --template-url https://$(BUCKET).s3.amazonaws.com/master.yml \
					--stack-name ${STACKNAME} \
					--parameters \
					ParameterKey=KeyName,ParameterValue=$(KEYFILE_ARG) \
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