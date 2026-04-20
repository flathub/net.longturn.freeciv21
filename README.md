# Flathub Flatpak for Freeciv21

Flathub is the central place for building and hosting Flatpak builds. This is the Freeciv21 Flatpak repository.
Refer to https://github.com/longturn/freeciv21 for more information.

Installing Freeciv21 from Flathub
---------------------------------

To install the `stable` version of Freeciv21 from Flathub, use the following:
```
flatpak remote-add flathub https://flathub.org/repo/flathub.flatpakrepo
flatpak install flathub net.longturn.freeciv21
```

To install the `non-stable` or `development` version of Freeciv21 from Flathub, use the following:
```
flatpak remote-add flathub-beta https://flathub.org/beta-repo/flathub-beta.flatpakrepo
flatpak install flathub-beta net.longturn.freeciv21
```

Freeciv21 Packaging Notes for Flathub
-------------------------------------

Start by setting up GitHub repositories on your local:

```
git clone git@github.com:longturn/net.longturn.freeciv21.git freeciv21-flatpak
cd freeciv21-flatpak
git remote add upstream https://github.com/flathub/net.longturn.freeciv21.git
git fetch upstream
git pull upstream master
git submodule init
git pull --recurse-submodules
```

The flathub repository has two main branches: `master` and `beta`. The `master` branch follows the `stable` 
branch in the main Freeciv21 code repository. Conversely, the `beta` branch follows the `master` branch in the 
main Freeciv21 code repository.

Install some software to build locally:

```
sudo apt install flatpak-builder
flatpak install flathub -y org.flatpak.Builder
```

Make needed updates to the manifest file: `net.longturn.freeciv21.yaml`.

Build locally:

```
# Run a linter on the manifest
flatpak run --command=flatpak-builder-lint org.flatpak.Builder manifest net.longturn.freeciv21.yaml

# Build the package
flatpak-builder --install-deps-from=flathub --force-clean build net.longturn.freeciv21.yaml

# Install to test
flatpak-builder --user --install --force-clean build net.longturn.freeciv21.yaml

# Run a test
flatpak run net.longturn.freeciv21

# Remove the local test
flatpak remove -y net.longturn.freeciv21
```
