# course-homework14

### task 1

```bash
echo "БЫЛО"
grep "BANN" lynis_before.txt | grep "^suggestion" || echo "check old file"

echo " СТАЛО"
sudo grep "^suggestion.*BANN" /var/log/lynis-report.dat || echo "Suggestions BANN-7126 и BANN-7130"
БЫЛО
check old file
 СТАЛО
Suggestions BANN-7126 и BANN-7130
```

---

### task 2

```bash
83c83
<   [WARNING]: Test DEB-0001 had a long execution: 13.736717 seconds
---
>   [WARNING]: Test DEB-0001 had a long execution: 14.041630 seconds
121,122c121,122
<   - Checking user password aging (minimum)                    [ DISABLED ]
<   - User password aging (maximum)                             [ DISABLED ]
---
>   - User password aging (minimum)                             [ CONFIGURED ]
>   - User password aging (maximum)                             [ CONFIGURED ]
144c144
<   Suggestions (11):
---
>   Suggestions (9):
180,189d179
<   * Configure minimum password age in /etc/login.defs [AUTH-9286]
<     - Related resources
<       * Article: Configure minimum password length for Linux systems: https://linux-audit.com/configure-the-minimum-password-length-on-linux-systems/
<       * Website: https://cisofy.com/lynis/controls/AUTH-9286/
<
<   * Configure maximum password age in /etc/login.defs [AUTH-9286]
<     - Related resources
<       * Article: Configure minimum password length for Linux systems: https://linux-audit.com/configure-the-minimum-password-length-on-linux-systems/
<       * Website: https://cisofy.com/lynis/controls/AUTH-9286/
<
215c205
<   Hardening index : 48 [#########           ]
---
>   Hardening index : 58 [###########         ]
```

---

### task 3

```bash
 cat index_before.txt
  Hardening index : 70 [##############      ]

┌──(kali㉿kali)-[~]
└─$ cat index_after2.txt
  Hardening index : 71 [##############      ]

sudo lynis audit system | grep "Hardening index" | tee index_after.txt
sudo grep -c "^suggestion" /var/log/lynis-report.dat
  Hardening index : 70 [##############      ]
45
$ sudo lynis audit system | grep "Hardening index" | tee index_after2.txt
sudo grep -c "^suggestion" /var/log/lynis-report.dat
  Hardening index : 71 [##############      ]
44


```

---

### task 4

```bash
user@debian:~/scap-security-guide-0.1.73$ sudo oscap xccdf eval \
  --profile xccdf_org.ssgproject.content_profile_anssi_np_nt28_minimal \
  --report ~/report_before.html \
  ssg-debian12-ds.xml 2>/dev/null | grep "Result" | sort | uniq -c
      5 faillt
     19 passlt
```

---

### task 5

```bash
Title   Ensure that official distribution repositories are used
Rule    xccdf_org.ssgproject.content_rule_apt_sources_list_official
Result  faill
Title   Enable syslog-ng Service
Rule    xccdf_org.ssgproject.content_rule_service_syslogng_enabled
Result  fail
Title   Ensure syslog-ng is Installed
Rule    xccdf_org.ssgproject.content_rule_package_syslogng_installed
Result  fail
Title   Enable rsyslog Service
Rule    xccdf_org.ssgproject.content_rule_service_rsyslog_enabled
Result  fail
Title   Ensure rsyslog is Installed
Rule    xccdf_org.ssgproject.content_rule_package_rsyslog_installed
Result  fail

```

---

```bash
sudo oscap xccdf eval   --profile xccdf_org.ssgproject.content_profile_anssi_np_nt28_minimal   ~/scap-security-guide-0.1.73/ssg-debian12-ds.xml 2>/dev/null | grep "fail"
Result  fail
Result  fail
Result  fail
Result  fail
```

---

### task 6

```bash
user@debian:~/scap-security-guide-0.1.73$ sudo systemctl enable --now syslog-ng
Synchronizing state of syslog-ng.service with SysV service script with /usr/lib/systemd/systemd-sysv-install.
Executing: /usr/lib/systemd/systemd-sysv-install enable syslog-ng
Created symlink '/etc/systemd/system/multi-user.target.wants/syslog-ng.service' → '/usr/lib/systemd/system/syslog-ng.service'.
user@debian:~/scap-security-guide-0.1.73$ echo "install usb-storage /bin/true" | sudo tee /etc/modprobe.d/disable-usb.conf
install usb-storage /bin/true
user@debian:~/scap-security-guide-0.1.73$ echo "* hard core 0" | sudo tee -a /etc/security/limits.conf
* hard core 0
user@debian:~/scap-security-guide-0.1.73$ sudo oscap xccdf eval \
  --profile xccdf_org.ssgproject.content_profile_anssi_np_nt28_minimal \
  ~/scap-security-guide-0.1.73/ssg-debian12-ds.xml 2>/dev/null | grep "Result" | sort | uniq -c
      3 faillt
     21 passlt


```

