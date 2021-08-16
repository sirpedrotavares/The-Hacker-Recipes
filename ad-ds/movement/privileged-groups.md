# Special groups

## Theory

> In the Windows Server operating system, there are several built-in accounts and security groups that are preconfigured with the appropriate rights and permissions to perform specific tasks. \([Microsoft](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn579255%28v=ws.11%29?redirectedfrom=MSDN)\)

There are scenarios where testers can obtain full control over members of built-in security groups. The usual targets are members of the "Administrators", "Domain Admins" or "Entreprise Admins" groups, however, other groups can sometimes lead to major privileges escalation.

## Practice

Below is a table summing up some groups' rights and abuse paths.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Security Group</th>
      <th style="text-align:left">Rights and abuses</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Account Operators</td>
      <td style="text-align:left">
        <p>its members can create and manage users and groups, including its own
          membership and that of the Server Operators group (e.g. <a href="access-control-entries/addmember.md">add a member to a group</a>)</p>
        <p></p>
        <p>&#x1F525;at the time of writing (12th, April 2021) members can sometimes
          also escalate through the &quot;Entreprise Key Admins&quot; group and obtain
          full control over the root domain (read <a href="https://secureidentity.se/adprep-bug-in-windows-server-2016/">the ADPREP bug</a>).</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Administrators</td>
      <td style="text-align:left">full admin rights to the Active Directory domain and Domain Controllers</td>
    </tr>
    <tr>
      <td style="text-align:left">Backup Operators</td>
      <td style="text-align:left">can backup or restore Active Directory and have logon rights to Domain
        Controllers</td>
    </tr>
    <tr>
      <td style="text-align:left">Server Operators</td>
      <td style="text-align:left">its members can sign-in to a server, start and stop services, access domain
        controllers, perform maintenance tasks (such as backup and restore), and
        they have the ability to change binaries that are installed on the domain
        controllers</td>
    </tr>
    <tr>
      <td style="text-align:left">DnsAdmins</td>
      <td style="text-align:left">can read, write, create, delete DNS records (e.g. edit the <a href="mitm-and-coerced-authentications/adidns-spoofing.md#manual-record-manipulation">wildcard record</a> if
        it already exists). Its members can also <a href="https://medium.com/@esnesenon/feature-not-bug-dnsadmin-to-dc-compromise-in-one-line-a0f779b8dc83">run code via DLL on a Domain Controller operating as a DNS server</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left">Domain Admins</td>
      <td style="text-align:left">full admin rights to the Active Directory domain, all computers, workstations,
        servers, users and so on</td>
    </tr>
    <tr>
      <td style="text-align:left">Entreprise Admins</td>
      <td style="text-align:left">full admin rights to all Active Directory domains in the AD forest</td>
    </tr>
    <tr>
      <td style="text-align:left">Group Policy Creators Owners</td>
      <td style="text-align:left">create Group Policies in the domain. Its members can&apos;t apply group
        policies to users or group or edit existing GPOs</td>
    </tr>
  </tbody>
</table>

## Resources

{% embed url="https://adsecurity.org/?p=3658" %}

{% embed url="https://docs.microsoft.com/en-us/troubleshoot/windows-server/identity/security-identifiers-in-windows" %}


