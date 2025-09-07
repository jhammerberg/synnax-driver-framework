# Synnax Driver Framework
A simple, easily adaptable Synnax driver in Python.

## Usage
0. Create a [Synnax deployment](https://docs.synnaxlabs.com/reference/cluster/quick-start) and confirm you can connect to it 
1. Clone this repo `git clone https://github.com/jhammerberg/synnax-driver-framework.git`
2. Download and install [uv](https://docs.astral.sh/uv/getting-started/installation/)
3. Go into the directory `cd synnax-driver-framework`
4. Sync the project & dependencies `uv sync`
5. Activate the project venv `source .venv/bin/activate` (different per OS)
6. Sign in to your Synnax cluster `sy login`
7. Run the driver `uv run synnax-driver` or just `./synnax-driver`

Enable logging with `-l` or `--log`:
```bash
./synnax-driver -l
```

Set a polling rate (default is 20) with `-r` or `--rate [rate]`:
```bash
./synnax-driver -r 50
```

See the help page with `-h` or `--help`:
```bash
./synnax-driver -h
```

## Modifying
This driver is meant to be modified and is moreso a template for what a real driver might want to do. To do this, create a global dictionary called `channels` with two items in it: `sensors` and `commands`. Each key in either `sensors` or `commands` should be a string paired with a function. The key will be the name of the channel in Synnax and the pair will be the the function whose return value will be sent to Synnax. For now, only binary command channels and float32 sensor channels are supported. An example for how to use this driver is provided and highlighted by comments.

To avoid having to having to sign in to your Synnax cluster each time the driver is ran, you can hard-code your Synnax credentials like this:
```py
client = sy.Synnax(
    host="example",
    port=9090,
    username="synnax",
    password="seldon",
    secure=False
)
```