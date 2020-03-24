You can combine multiple inventory files, for example, from different
data centers, into a single file in order to generate a single Migration
Analytics report.

  - You must ensure that the inventory files do not contain duplicate
    information.

<!-- end list -->

1.  Log in to the CloudForms machine.

2.  Create a common directory for the extracted inventory files:
    
        # mkdir extracted_files

3.  Extract an inventory file to the common directory:
    
        # tar -xvf <inventory_file_name>.tar.gz -C extracted_files/ 
    
      - Specify the inventory file name.

4.  Rename the extracted JSON inventory file. Each file name must be
    unique.

5.  Create a new archive file containing the extracted inventory files:
    
        # tar -czvf <new_archive>.tar.gz extracted_files/ 
    
      - Specify the new archive file name.

You can browse to the new archive file when you create a Migration
Analytics report.
