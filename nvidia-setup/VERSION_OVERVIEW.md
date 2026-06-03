# 0.1.x

| service | accelerator | kernel              | efa         | chrony | raid0 | OFI |
|---------|-------------|---------------------|-------------|--------|-------|-----|
| eks     | h100        | 6.14.0-1018-aws     | 1.47.0      |  Y     |  Y    |  N  |
| eks     | gb200       | 6.14.0-1018-aws     | 1.47.0      |  Y     |  Y    |  N  |

# 0.2.x

| service | accelerator | kernel              | efa         | chrony | raid0 | OFI |
|---------|-------------|---------------------|-------------|--------|-------|-----|
| eks     | h100        | 6.14.0-1018-aws     | 1.47.0      |  Y     |  Y    |  Y  |
| eks     | gb200       | 6.14.0-1018-aws     | 1.47.0      |  Y     |  Y    |  Y  |

# 0.3.x

Adds the `bcm` service. `service=bcm`'s sole job is to alias `/usr/src/linux-$(uname -r)` to the Ubuntu `linux-headers-$(uname -r)` tree so consumers reading `/usr/src/linux-$(uname -r)/.config` find it (AICR #1093). For `service=bcm` the apply stage skips the kernel/EFA pipeline and runs only this single step.

| service | accelerator | kernel              | efa         | chrony | raid0 | OFI | bcm headers alias |
|---------|-------------|---------------------|-------------|--------|-------|-----|-------------------|
| eks     | h100        | 6.14.0-1018-aws     | 1.47.0      |  Y     |  Y    |  Y  |  N                |
| eks     | gb200       | 6.14.0-1018-aws     | 1.47.0      |  Y     |  Y    |  Y  |  N                |
| bcm     | h100        | n/a                 | n/a         |  N     |  N    |  N  |  Y                |
| bcm     | gb200       | n/a                 | n/a         |  N     |  N    |  N  |  Y                |

# 0.4.x

Adds the `vr200` accelerator (gb200 hardware on the 6.17 kernel). `eks-vr200`
mirrors `eks-gb200` but pins kernel `6.17.0-1017-aws`. `bcm-vr200` behaves like
`bcm-gb200` (kernel-headers alias only; no kernel/EFA/lustre baked in).

| service | accelerator | kernel              | efa         | chrony | raid0 | OFI | bcm headers alias |
|---------|-------------|---------------------|-------------|--------|-------|-----|-------------------|
| eks     | h100        | 6.14.0-1018-aws     | 1.47.0      |  Y     |  Y    |  Y  |  N                |
| eks     | gb200       | 6.14.0-1018-aws     | 1.47.0      |  Y     |  Y    |  Y  |  N                |
| eks     | vr200       | 6.17.0-1017-aws     | 1.47.0      |  Y     |  Y    |  Y  |  N                |
| bcm     | h100        | n/a                 | n/a         |  N     |  N    |  N  |  Y                |
| bcm     | gb200       | n/a                 | n/a         |  N     |  N    |  N  |  Y                |
| bcm     | vr200       | n/a                 | n/a         |  N     |  N    |  N  |  Y                |