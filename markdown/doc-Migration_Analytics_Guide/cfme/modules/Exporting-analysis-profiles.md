You can export your analysis profiles for backup, troubleshooting, or
updating.

1.  Log in to the CloudForms machine as root.

2.  Go to the `vmdb` directory:
    
        # cd /var/www/miq/vmdb

3.  Create an export directory:
    
        # mkdir exports

4.  Export the analysis profiles:
    
        # bundle exec rake evm:export:scan_profiles -- --directory exports --all 
    
      - The `--all` option exports all the analysis profiles as `yaml`
        files. There is no option to export a single analysis profile.
