# OpenArm KER

A teleoperation system for OpenArm robots using KER (Kinematic Equivalent Replica).

## Features

- **Joint mapping**: Flexible configuration-based mapping from leader to follower joints
- **Serial communication**: Interface with m5stack-cores3 via uart

## Quick start

### Install

```bash
pip install openarm_ker
```

### Sample usage

```python
import numpy as np
import openarm_ker

m5_port = openarm_ker.M5Port("/dev/ttyACM0")

leader_joint_names = [f"arm_joint{i}" for i in range(1, 9)]
mapper = openarm_ker.Mapper(
    mappingyaml_path="/path/to/mapping_m5.yaml",
    leader_joint_names=leader_joint_names,
    mapping_key="right_arm_mappings",
)

m5_port.fetch_present_status_bulk()
leader_position = m5_port.present_position
follower_position = mapper.map(np.deg2rad(leader_position))
```

### Mapper config

Please refer to [config/](config/), the default configurations.

## Related links

- 📚 Read the [documentation](https://docs.openarm.dev/software/can/)
- 💬 Join the community on [Discord](https://discord.gg/FsZaZ4z3We)
- 📬 Contact us through <openarm@enactic.ai>

## License

Licensed under the Apache License 2.0. See [LICENSE.txt](LICENSE.txt) for details.

Copyright 2026 Enactic, Inc.

## Code of Conduct

All participation in the OpenArm project is governed by our [Code of Conduct](CODE_OF_CONDUCT.md).
