# AWS_EKS_Cluster
This repository contains code for deploying an AWS EKS cluster

__NOTE:__
- This Cluster is provisioned in the us-east-2 region with eksctl using the eks-cluster file which also creates the managed-cluster and two Auto Scaling Group (ng-1 and ng-2) stacks.
- AllowExternalDNSUpdateIAM policy gives ExternalDNS the necessary IAM permissions to view and manage the hosted zone and it was performed via the AWS web console.
- aws-auth-configmap file contains RBAC configuration for the cluster and it is used to grant additional users and roles the ability to interact with the cluster.
- ec2-asg-policy file includes the required policy needed by EKS to manage worker nodes for auto scaling. 
- eks-cluster file contains detailed information about the cluster as well as the Auto Scaling Groups.
- externalDnsManifest file is used to create the External DNS which allows the cluster to automatially update DNS records in the code-challenge-test.com private zone which was manually created using the AWS Web Console. A secret that the external DNS uses to communicate with the API for correct level of access was separated created, but not documented here.
- namespace file contains information about user-1 and user-2 namespaces. The default namespace was initially created during cluster creation.
- nginxConfig manifest is used to test user permission by attempting to create an Nginx pod in a specific namespace.
- IAM Role for Kubernetes resources creation was done using the AWS web console and assigned below policy to the dev-user:
  1. AmazonEC2FullAccess
  2. IAMFullAccess
  3. AmazonVPCFullAccess
  4. CloudFormation-Admin-policy
  5. EKS-Admin-policy
- dev-user, andi, and pete users were created using the AWS Web Console.
- user role manifest file includes the Roles/ClusterRole, Rolebinding/ClusterRoleBinding for andi, pete, and dev-user.
- nginx-externalDNStest manifest will create nginx service for testing 
