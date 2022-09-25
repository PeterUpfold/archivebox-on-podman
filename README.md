# archivebox-on-podman

**This is a horrible quick hack to get ArchiveBox to build under rootless podman.** I am learning `podman`, including rootless, and I am almost certainly doing things wrong. You should not use this.

If you are content to use this messy approach, it is absolutely at your own risk.

    podman run --user SOME_USER_ID --volume /path/to/archivebox/data:/data localhost/archivebox-on-podman server
    

## Permissions on `data` directory

Outside of containerland, ensure chowned to the rootless podman-running user.

Then:

    podman unshare chown -R SOME_USER_ID:SOME_USERID /path/to/archivebox/data

## Adding new import

    archivebox server
    podman ps
    podman run --rm -i --user SOME_USER_ID --volume /path/to/archivebox/data:/data localhost/archivebox-on-podman add < ~/somefile

## Regular rebuild

Rebuild when a new critical fix in Chromium is released, as well as other dependent packages.

    podman build --squash -t localhost/archivebox-on-podman .
