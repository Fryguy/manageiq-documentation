1.  Log in to Red Hat OpenStack Platform.

2.  [Resize the conversion host
    instance](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/16.0/html-single/instances_and_images_guide/index#section-resize-instance)
    to accommodate its file system.
    
    The conversion host instance is created from an image, but the disk
    space defined in the image is not sufficient. You can either extend
    the partition (and subsequently, extend the physical volume in the
    volume group) to the required size or you can create a new partition
    and add it as a physical volume to the volume group.
    
    <div class="note">
    
    You must resize `lv_root` to use all available disk space because
    the image will not use it by default.
    
    </div>
