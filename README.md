# Lightning Components

This is "working" for me locally - "working" in the sense that I don't get any
errors or notices. DF does seem broken though (even without the Lightning
modules installed). I noticed that the bundled version on D.O hasn't been
updated since June, so we should probably fix that before troubleshooting
further.

I did some shuffling to get the most recent version of core and the lightning
modules into DF. Rather than try to explain it, I've just included my
GNUmakefile below:

    all:
      drush dl df --drupal-project-rename=df -y
      drush dl drupal --drupal-project-rename=docroot -y
      cp -r df/profiles/df docroot/profiles/df
      rm -rf df
      cp -r -p build/ docroot/modules/lightning_components
      drush make build/lightning_workflow/lightning-workflow.make.yml docroot/ --no-core
      drush make build/lightning_layout/lightning-layout.make.yml docroot/ --no-core
      cd docroot; \
      drush si df -y --account-pass=df --site-name='DF + Lightning Components' --db-url=mysql://root:root@127.0.0.1/df; \
      drush en lightning_layout -y; \
      drush en lightning_workflow -y

