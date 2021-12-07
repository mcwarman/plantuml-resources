# plantuml-resources

## AWS Group Icons

```plantuml
@startuml

!define PUMLResources https://raw.githubusercontent.com/mcwarman/plantuml-resources/main/src
!include PUMLResources/AWSGroupIcons.puml
!include PUMLResources/Hidden.puml

!define AWSPuml https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v11.1/dist


!include AWSPuml/Compute/EC2AutoScaling.puml
!include AWSPuml/Compute/EC2Instance.puml

!include AWSPuml/GroupIcons/AutoScalingGroup.puml

!include AWSPuml/NetworkingContentDelivery/VPCNATGateway.puml

CloudGroup(cloud, "AWS Cloud") {
  VirtualPrivateCloudVPCGroup(vpc, "VPC") {

    AvalabilityZoneGroup(az_2, "Availability Zone 2") {
      VPCNATGateway(az_2_nat_gateway, "NAT Gateway", "")
      EC2Instance(az_2_ec2_1, "Instance", "")
      EC2Instance(az_2_ec2_2, "Instance", "")
      az_2_nat_gateway -[hidden]d- az_2_ec2_1
      az_2_ec2_1 -[hidden]d- az_2_ec2_2
    }

    HiddenRectangle(hidden_rectangle) {
      EC2AutoScaling(ec2_auto_scaling, "Amazon EC2 Auto Scaling", "")
      AutoScalingGroup(asg_1, "Auto Scaling Group", "")
      AutoScalingGroup(asg_2, "Auto Scaling Group", "")
      ec2_auto_scaling -[hidden]d- asg_1
      asg_1 -[hidden]d- asg_2
    }

    AvalabilityZoneGroup(az_1, "Availability Zone 1") {
      VPCNATGateway(az_1_nat_gateway, "NAT Gateway", "")
      EC2Instance(az_1_ec2_1, "Instance", "")
      EC2Instance(az_1_ec2_2, "Instance", "")
      az_1_nat_gateway -[hidden]d- az_1_ec2_1
      az_1_ec2_1 -[hidden]d- az_1_ec2_2
    }

    ec2_auto_scaling -[hidden]l- az_1_nat_gateway
    ec2_auto_scaling -[hidden]r- az_2_nat_gateway

    asg_1 -[dashed,#D86613]l- az_1_ec2_1
    asg_1 -[dashed,#D86613]r- az_2_ec2_1

    asg_2 -[dashed,#D86613]l- az_1_ec2_2
    asg_2 -[dashed,#D86613]r- az_2_ec2_2

  }
}
@enduml

```
