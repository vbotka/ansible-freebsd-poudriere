.. _ug_idempotent:

Idempotent role
---------------

The role is idempotent. For example, if Poudriere is configured to build packages for two architectures ::

   poudriere_pkg_arch: [amd64, arm]

there should be no changes reported when the playbook is run repeatedly with the same data ::

   shell> ANSIBLE_DISPLAY_OK_HOSTS=false ANSIBLE_DISPLAY_SKIPPED_HOSTS=false ansible-playbook pb.yml

   PLAY [build.example.com] *******************************************************************************
   included: /home/admin/.ansible/roles/vbotka.freebsd_poudriere/tasks/pkglist.yml for build.example.com => (item=amd64)
   included: /home/admin/.ansible/roles/vbotka.freebsd_poudriere/tasks/pkglist.yml for build.example.com => (item=arm)

   PLAY RECAP *********************************************************************************************
   build.example.com: ok=13   changed=0    unreachable=0    failed=0    skipped=12   rescued=0    ignored=0
