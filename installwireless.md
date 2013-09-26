t worked like a CHARM
    Brief of what i did for further reference.

    sudo apt-get install linux-headers-generic build-essential

    https://www.kernel.org/pub/linux/ker...kports/stable/
    Downloaded and extracted; compat-drivers-3.9-rc4-2-s.tar.bz2

    cd Desktop/compat-drivers-3.9-rc4-2-s
    sudo su
    ./scripts/driver-select ath9k
    make


    I got one error after this command, the error was
    error: redefinition of ‘kref_get_unless_zero’
    include/linux/kref.h:47:32: note: previous definition of ‘kref_get_unless_zero’ was here

    Then i did this in one of file

    open the file .../compat-wireless-2012-12-18/include/linux/compat-3.8.h in your favourite editor,
    find the kref_get_unless_zero function (telling from your error message, it should be on line 47) and comment it out. In case you have no idea what I'm talking about: Comment this code


    static inline int __must_check kref_get_unless_zero(struct kref *kref)
    {
    return atomic_add_unless(&kref->refcount, 1, 0);
    }

    then

    carry on with

    make
    make install
    modprobe ath9k
    exit

    after a reboot , my wifi is working like a charm.....

    Thanks
    Anoop 


