# SM-P205 LineageOS 20 Manifest

Public local manifest for building LineageOS 20 for the Samsung Galaxy Tab A
8.0 with S Pen LTE (`SM-P205`, `p205` / `wisdom`).

This manifest intentionally does not include proprietary vendor repositories.
Users must extract proprietary blobs locally from Samsung stock firmware or from
a compatible device.

## Sync

```bash
mkdir lineageos20-p205
cd lineageos20-p205

repo init -u https://github.com/LineageOS/android.git -b lineage-20.0 --git-lfs
mkdir -p .repo/local_manifests
curl -L https://raw.githubusercontent.com/xuanyayi/android_manifest_samsung_p205/lineage-20-p205/wisdom.xml \
  -o .repo/local_manifests/wisdom.xml

repo sync -c -j"$(nproc --all)" --force-sync --no-clone-bundle --no-tags
```

## Extract Blobs

```bash
adb root
cd device/samsung/p205
./extract-files.sh
```

Or extract from an unpacked stock firmware directory:

```bash
cd device/samsung/p205
./extract-files.sh /path/to/unpacked/firmware
```

## Apply Platform Patches

```bash
cd /path/to/lineageos20-p205
git clone https://github.com/xuanyayi/android_patches_samsung_p205 -b lineage-20-p205 p205-patches
./p205-patches/apply-patches.sh "$PWD"
```

## Build

```bash
source build/envsetup.sh
lunch lineage_p205-userdebug
mka bacon
```
