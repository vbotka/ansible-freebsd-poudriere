.. _ug_idempotent:

Idempotent role
---------------

Except of the certificate's generation, the role is idempotent. The goal is to run the playbook
without any changes after Poudriere is installed and configured, e.g. ::

  shell> ANSIBLE_DISPLAY_OK_HOSTS=false ANSIBLE_DISPLAY_SKIPPED_HOSTS=false ansible-playbook pb.yml

  PLAY [build.example.com] *******************************************************************************
  included: /home/admin/.ansible/roles/vbotka.freebsd_poudriere/tasks/pkglist.yml for build.example.com

  PLAY RECAP *********************************************************************************************
  build.example.com: ok=10   changed=0    unreachable=0    failed=0    skipped=12   rescued=0    ignored=0
