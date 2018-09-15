# KVM Installation and Troubleshooting

## Can’t Access KVM from virt-manager on remote Ubuntu install

**First Issue**: need ssh-askpass package.

Error says to install openssh-askpass, but on Ubuntu package is name
“ssh-askpass”.

**Second Issue**: can’t verify host key.

Because virt-manager is trying to connect via ssh, need to get key accepted.
Can’t accept key via virt-manager, so quickest solution is to just ssh to the
host, accept the key, then exit out, then try to connect to KVM.

**Third Issue**: getting error “authentication unavailable: no polkit agent
available to authenticate action ‘org.libvirt.unix.manage'”.

Solution: add the ssh user to the libvirt group.

Source: http://blog.wikichoon.com/2016/01/polkit-password-less-access-for-libvirt.html
