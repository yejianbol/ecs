# DeleteInstance {#DeleteInstance .reference}

Release aPay-As-You-Go or expired Subscription instance.

## Description {#section_bvk_f4s_xdb .section}

-   You can only release an instance that is in the **Stopped** \(`Stopped`\) status.

-   After the instance is released, all the physical resources used by the instance are recycled, removed, and impossible to recover. The attached cloud disks with the property of `DeleteWithInstance=True` are also released. The automatic snapshots of these disks with  the property of `DeleteAutoSnapshot` being `DeleteAutoSnapshot=false` are retained, and automatic snapshots with the property of  `DeleteAutoSnapshot=true` are released.

-   If the instance is under [security control](reseller.en-US/API Reference/Appendix/API behavior when an instance is locked for security reasons.md#) and `OperationLocks` indicates `"LockReason" : "security"`, even if the property of `DeleteWithInstance` is `False`, its attached cloud disks will be ignored and released directly.


## Request parameters {#RequestParameter .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The name of this interface. Value: DeleteInstance.|
|InstanceId|String|Yes|ID of an instance.|

## Response parameters {#ResponseParameter .section}

For more information about all the common response parameters, see [Common parameters](reseller.en-US/API Reference/Getting started/Common parameters.md#commonResponseParameters).

## Examples { .section}

**Request example** 

```
https://ecs.aliyuncs.com/?Action=DeleteInstance
&InstanceId=i-instance1
&<Common Request Parameters>
```

**Response example** 

**XML format**

```
<DeleteInstanceResponse>
    <RequestId>928E2273-5715-46B9-A730-238DC996A533</RequestId>
</DeleteInstanceResponse>
```

 **JSON format** 

```
{
    "RequestId": "928E2273-5715-46B9-A730-238DC996A533"
}
```

## Error codes {#ErrorCode .section}

|Error code|Error message|HTTP status code|Meaning|
|:---------|:------------|:---------------|:------|
|DependencyViolation.RouteEntry|Specified instance is used by route entry.|400|The specified instance is used by the service [Route entry](../../../../reseller.en-US/User Guide/Routing.md#).|
|DependencyViolation.SLBConfiguring|Specified operation is denied as your instance is using by another product.|400|The specified instance is used by the service [Server Load Balancer](../../../../reseller.en-US/Product Introduction/What is Server Load Balancer?.md#).|
|InvalidParameter|The input parameter InstanceId is invalid.|400|The specified instance ID is invalid.|
|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|403|You cannot release an in service subscribed instance.|
|InvalidOperation.DeletionProtection|The operation is not allowed due to “\{0\}” is protected by deletion protection.|400|The specified instance cannot be deleted as deletion protection is enabled for it.|
|IncorrectInstanceStatus|The current status of the resource does not support this operation.|403|You can only release an instance that is in the **Stopped** \(`Stopped`\) status.|
|IncorrectInstanceStatus.Initializing|The specified instance status does not support this operation.|403|The specified instance is being created. Please try again later.|
|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|403|Your instance is locked out of security.|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|The specified instance does not exist.|

