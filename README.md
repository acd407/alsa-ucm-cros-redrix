# alsa-ucm-cros-redrix

Google Redrix（Chromebook, `sof-rt5682` 声卡）的 ChromeOS UCM 配置 Arch 打包。

## 内容

把 `chromebook-linux-audio` 脚本安装的、不被任何 pacman 包管理的 11 个 UCM 文件收编成 Arch 包：

```
platforms/intel-sof/platform.conf
platforms/intel-sof/codecs.conf
codecs/max98390/init.conf
codecs/max98390/speaker.conf
codecs/hda/hdmi2345.conf
codecs/rt5682s/init.conf
codecs/rt5682s/headset.conf
conf.d/sof-rt5682/sof-rt5682.conf
conf.d/sof-rt5682/HiFi.conf
conf.d/sof-rt5682/rt5682-init.conf
conf.d/sof-rt5682/rt5682-headset.conf
```

## 说明

- 来源：[WeirdTreeThing/alsa-ucm-conf-cros](https://github.com/WeirdTreeThing/alsa-ucm-conf-cros)（standalone 分支）
- `HiFi.conf` 已相对上游修改：**删除了 `SectionDevice."Mic2"`**。Redrix 只有 2 个麦克风（ch0/ch1，PDM0），Mic2 对应的 ch2/ch3 是未接的 PDM1 空通道。原配置会产生虚假的 "Internal Microphone 2" 节点，并与 Mic1 共用同名 `dmic_stereo_in` dsnoop 造成通道串扰。
- 安装位置：`/usr/share/alsa/ucm2/`（与 `alsa-ucm-conf` 包无冲突，这些路径不被任何包拥有）

## 构建与安装

```bash
makepkg -f
pacman -U alsa-ucm-cros-redrix-*.pkg.tar.*
```

验证：

```bash
pacman -Qkk alsa-ucm-cros-redrix
```

## 更新流程

上游 UCM 更新后：

1. 用新文件覆盖相应目录（`codecs/`、`conf.d/`、`platforms/`）
2. 重新审视 `HiFi.conf` 的 Mic2 修改是否仍需要
3. 提升 `pkgver`/`pkgrel`
4. `makepkg -f` 后 `pacman -U` 升级

## 注意

重跑 `chromebook-linux-audio/setup-audio` 会以 root 覆盖这些文件，导致 `pacman -Qkk` 报 MODIFIED。如需防覆盖，可将相关路径加入 `pacman.conf` 的 `NoUpgrade`。

## 机型

- 主板：`Google_Brya`（Alder Lake）
- 声卡：`sof-rt5682`（MAX98390 功放 + RT5682s 耳机）
- 拓扑：`intel/sof-tplg/sof-adl-max98390-rt5682.tplg`