# Samsung wisdom LineageOS 20 Manifest

Public local manifest for building LineageOS 20 for the Samsung Galaxy Tab A
8.0 with S Pen LTE (`SM-P205`, codename `wisdom`).

The proprietary vendor repositories are public and included in this manifest, so
users do not need to extract blobs before building.

## Sync

```bash
mkdir lineageos20-wisdom
cd lineageos20-wisdom

repo init -u https://github.com/LineageOS/android.git -b lineage-20.0 --git-lfs
mkdir -p .repo/local_manifests
curl -L https://raw.githubusercontent.com/xuanyayi/android_manifest_samsung_wisdom/lineage-20/wisdom.xml \
  -o .repo/local_manifests/wisdom.xml

repo sync -c -j"$(nproc --all)" --force-sync --no-clone-bundle --no-tags
```

## Apply Platform Patches

```bash
cd /path/to/lineageos20-wisdom
./patches/samsung/wisdom/apply-patches.sh "$PWD"
```

## Build

```bash
source build/envsetup.sh
lunch lineage_wisdom-userdebug
mka bacon
```
