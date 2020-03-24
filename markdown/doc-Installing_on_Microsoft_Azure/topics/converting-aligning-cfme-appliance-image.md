# Converting and Aligning the {product-title\_short} Virtual Appliance Image

Complete the following procedure to ensure the {product-title\_short}
dynamic .vhd file is properly aligned to the nearest 1 MB boundary, and
is in a fixed-size VHD format.

1.  Convert the dynamic VHD file you downloaded in
    [???](#obtaining-the-appliance) to RAW format.
    
        $ qemu-img convert -f vpc -O raw <image-name.vhd> <image-name.raw>
        
        Example:
        
        $ qemu-img convert -f vpc -O raw example.vhd rexample.raw

2.  Copy and paste the script below into a new bash shell script file,
    for example, `aligned-size.sh`. Change *rawdisk="image-name"* to the
    image name for your file. This script will calculate the rounded
    file size to the nearest 1 MB boundary.
    
        #!/bin/bash
        rawdisk="example.raw"
        MB=$((1024 * 1024))
        size=$(qemu-img info -f raw --output json "$rawdisk" | gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')
        rounded_size=$((($size/$MB + 1) * $MB))
        echo "rounded size = $rounded_size"
        export rounded_size

3.  Run the shell script. The file name `aligned-size.sh` is used in
    this example.
    
        $ sh aligned-size.sh
        
        rounded size = 34361835520

4.  Resize the virtual appliance image using the rounded size.
    
        $ qemu-img resize -f raw <image-name.raw> <rounded_size>
        
        Example:
        
        $ qemu-img resize -f raw example.raw 34361835520
        
        Image resized.

5.  Convert the appliance image to a fixed-size VHD file.
    
        $ qemu-img convert -f raw -o subformat=fixed -O vpc <image-name.raw> <image-name.vhd>
        
        Example:
        
        qemu-img convert -f raw -o subformat=fixed -O vpc example.raw example.vhd

6.  Get the virtual size for the VHD file.
    
        $ qemu-img info --output=json -f vpc <path-to-image>
        
        Example:
        
        $ qemu-img info --output=json -f vpc example.vhd
        
        {
          "virtual-size": 34361835520,
          "filename": "example.vhd",
          "cluster-size": 2097152,
          "format": "vpc",
          "actual-size": 2133401600,
          "dirty-flag": false
        }

7.  Divide the virtual-size value by 1024, twice. If the result is a
    whole number, the VHD file is aligned properly. The example below
    shows that the file is properly aligned.
    
        34361835520 / 1024 / 1024 = 32770

<div class="important">

qemu-img version 1.5.3 is used in this procedure. Check the qemu-img
version using the command: `yum info qemu-img`. If the version is 2.2.1
or later, add the option *force\_size* in the conversion command, for
example, *subformat=fixed,force\_size*.

</div>

The {product-title} Azure virtual appliance image is ready for uploading
and provisioning in Microsoft Azure.
