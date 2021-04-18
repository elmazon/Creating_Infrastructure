# Creating_Infrastructure
# Use the latest 2.1 version of CircleCI pipeline process engine. See: https://circleci.com/docs/2.0/configuration-reference
version: 2.1
jobs:
  create_infrastructure:
    docker:
      - image: amazon/aws-cli
    steps:
      - checkout
      - run:
          name: Ensure backend infrastructure exist
          command: |
            aws cloudformation deploy \
              --template-file template.yml \
              --stack-name my-stack 
workflows:
  my_workflow:
    jobs:
      - create_infrastructure:
          context : AWS