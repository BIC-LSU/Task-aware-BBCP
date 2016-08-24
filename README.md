# Task-aware-BBCP
## BaBar CP (BBCP) with Task-awareness Enhancement

The task-aware [BBCP](https://www.slac.stanford.edu/~abh/bbcp/) for the BIC-LSU project sends a scheduling request which contains all TCP connections used in the current transmission task to the SDN scheduler for network scheduling optimization.

## Augmented Command Line Arguments

**-J \<validation string>,\<scheduler interface>,\<scheduler interface IP version>,\<scheduler port>,\<reporter>**

**\<validation string>**: A given string for validating the scheduling request at the scheduler.<br />
**\<scheduler interface>**: The FQDN or IP Address of the listening interface for the scheduler.<br />
**\<scheduler interface IP version>**: The IP Address version of the listening interface. Valid values "IPv4" and "IPv6".<br />
**\<scheduler port>**: The port number of the listening port for the scheduler.<br />
**\<reporter>**: The process which should send the scheduling request. Valid values "src" and "dst".<br />
If any error occurs in the task-awareness related code segments, task-aware BBCP degrades to the regular BBCP.<br />

## The Scheduling Request

The scheduling request is a JSON string in the following format generated by the [cJSON](https://github.com/DaveGamble/cJSON) library.
```
{
    "validation": <validation code>,
    "size": <task size>,
    "flow": {
        "sip": <source IP>,
        "dip": <destination IP>,
        "port": [
            {"sp": <src port>, "dp": <dst port>},
            ...
        ]
    }
}
```
