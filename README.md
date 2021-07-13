# aws-lambda-cli-layer
aws lambda layer for usage of aws cli in lambda

create layer in lambda, python 3.8

create lambda and add this layer


example code to call aws cli :

            import subprocess
            import logging

            logger = logging.getLogger()
            logger.setLevel(logging.INFO)

            def run_command(command):
                command_list = command.split(' ')
                try:
                    logger.info("Running shell command: \"{}\"".format(command))
                    result = subprocess.run(command_list, stdout=subprocess.PIPE);
                    logger.info("Command output:\n---\n{}\n---".format(result.stdout.decode('UTF-8')))
                except Exception as e:
                    logger.error("Exception: {}".format(e))
                    return False
                return True

            def handler(event, context):
                run_command('/opt/aws --version')
