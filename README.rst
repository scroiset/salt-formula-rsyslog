
==================================
rsyslog
==================================

In computing, syslog is a widely used standard for message logging. It permits separation of the software that generates messages, the system that stores them, and the software that reports and analyzes them.

Sample pillars
==============

Rsyslog service with default logging template

.. code-block:: yaml

    rsyslog:
      client:
        enabled: true


Rsyslog service with precise timestamps, severity, facility.

.. code-block:: yaml

    rsyslog:
      client:
        enabled: true
        format:
          name: TraditionalFormatWithPRI
          template: '"%syslogpriority% %syslogfacility% %timestamp:::date-rfc3339% %HOSTNAME% %syslogtag%%msg:::sp-if-no-1st-sp%%msg:::drop-last-lf%\n"'
        logfiles:
          file:
            -/var/log/syslog:
              filter: *.*;auth,authpriv.none
              owner: syslog
              group: adm
              createmode: 0640
              umask: 0022
            /var/log/auth.log:
              filter: auth,authpriv.*
              owner: syslog
              group: adm
              createmode: 0640
              umask: 0022
            -/var/log/kern.log:
              filter: kern.*
              owner: syslog
              group: adm
              createmode: 0640
              umask: 0022
           -/var/log/mail.log:
              filter: mail.*
              owner: syslog
              group: adm
              createmode: 0640
              umask: 0022
            /var/log/mail.err:
              filter: mail.err
              owner: syslog
              group: adm
              createmode: 0640
              umask: 0022
            ":omusrmsg:*":
              filter: *.emerg
            "|/dev/xconsole":
              filter: "daemon.*;mail.*; news.err; *.=debug;*.=info;*.=notice;*.=warn":


Read more
=========

http://www.rsyslog.com/
https://wiki.gentoo.org/wiki/Rsyslog
https://github.com/saz/puppet-rsyslog

Documentation and Bugs
======================

To learn how to install and update salt-formulas, consult the documentation
available online at:

    http://salt-formulas.readthedocs.io/

In the unfortunate event that bugs are discovered, they should be reported to
the appropriate issue tracker. Use Github issue tracker for specific salt
formula:

    https://github.com/salt-formulas/salt-formula-rsyslog/issues

For feature requests, bug reports or blueprints affecting entire ecosystem,
use Launchpad salt-formulas project:

    https://launchpad.net/salt-formulas

You can also join salt-formulas-users team and subscribe to mailing list:

    https://launchpad.net/~salt-formulas-users

Developers wishing to work on the salt-formulas projects should always base
their work on master branch and submit pull request against specific formula.

    https://github.com/salt-formulas/salt-formula-rsyslog

Any questions or feedback is always welcome so feel free to join our IRC
channel:

    #salt-formulas @ irc.freenode.net
