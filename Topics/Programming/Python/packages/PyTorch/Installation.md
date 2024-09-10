Installing PyTorch can be as simple as
```shell
pip install torch
```

> [!caution]
On a Linux system this will automatically get a CUDA enabled installation of `torch` if possible, but on Windows this will _always_ install the CPU only version. To install the CUDA version of `torch` on Windows, see the [getting started page](https://pytorch.org/get-started/locally/) and select the CUDA version that you have installed, or the one nearest but not greater, than the version you have installed.
> For example, with CUDA 12.4, the command will be
> ```shell
> pip install torch --index-url https://download.pytorch.org/whl/cu124
> ```
> If you already accidentally installed the CPU version of `torch`, add `-U` or `--upgrade` to your `pip install` command:
> ```shell
> pip install -U torch --index-url https://download.pytorch.org/whl/cu124
> ```