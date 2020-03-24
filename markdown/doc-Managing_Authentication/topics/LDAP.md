Select **LDAP** or **LDAPS** to configure {product-title\_short}
authentication using Red Hat Identity Management (IdM), Active
Directory, or another identity management service that uses LDAP
protocol.

If you choose LDAP or LDAPS as your authentication mode, the required
parameters are exposed under **LDAP Settings**. Be sure to validate your
settings before saving them.

<div class="important">

This procedure requires a preconfigured authentication system such as
Red Hat Identity Management (IdM) or Active Directory (AD) with user
groups configured.

</div>

LDAP authentication for {product-title\_short} requires group membership
to be defined by the LDAP RFC 2307 schema, where group members are
listed by name in the member UID attribute.

For more information about Red Hat Identity Management, see the [Linux
Domain Identity, Authentication, and Policy
Guide](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/linux_domain_identity_authentication_and_policy_guide/index)
and related Red Hat Enterprise Linux documentation.

# Configuring LDAP or LDAPS Authentication

To configure {product-title\_short} to use LDAP for authentication:

1.  Click ![config gear](config-gear.png) (**Configuration**).

2.  Select your server in the **Settings** accordion.

3.  Select the **Authentication** tab.

4.  Select a **Session Timeout** to set the period of inactivity before
    a user is logged out of the console.

5.  Select **LDAP** or **LDAPS** from the **Mode** list. This exposes
    additional required parameters under **LDAP Settings**.

6.  Configure your **LDAP Settings** (the following example configures
    an IdM directory server):
    
      - Use **LDAP Host Names** to specify the fully qualified domain
        names of your directory servers. {product-title\_short} will
        search each host name in order until it finds one that
        authenticates the user. Note, {product-title\_short} supports
        using a maximum of three possible **LDAP Host Names**.
    
      - Use **LDAP Port** to specify the port for your directory server.
        The default is 389 for LDAP and 636 for LDAPS.
    
      - From the **User Type** list, select one of the following and
        configure the values for your directory server:
        
          - **User Principal Name**: Type the user name in the format of
            *user@domainname*, for example, *dbright@acme.com*. (In this
            case, the user would log on as *dbright*.)
        
          - **Email Address**: Logs in with the user’s email address.
        
          - **Distinguished Name** (CN=\<user\>): Uses the common name
            for the user. Be sure to enter the correct **User Suffix**
            and **Distinguished Name** option for your directory service
            implementation: for example, *cn=dan
            bright,ou=users,dc=acme,dc=com*. (The user logs on as *dan
            bright*.)
        
          - **Distinguished Name** (UID=\<user\>): Uses the user ID
            (UID). Be sure to enter the correct **User Suffix** and
            **Distinguished Name** option for your directory service
            implementation: for example, *uid=dan
            bright,ou=users,dc=acme,dc=com*. (The user logs on as *dan
            bright*.)
        
          - **SAM Account Name**: User logon for Active Directory
            clients and servers using legacy Windows versions. You must
            also configure the **Domain Prefix** in the next field when
            selecting this option.
    
      - Specify the **Domain Prefix** if you are configuring an Active
        Directory LDAP host, and selected **SAM Account Name** as the
        **User Type**. This field represents the prefix name in the
        Active Directory domain. Together with the SAM account name,
        this constructs the fully qualified user name in the format
        `<domain_prefix>\<user>`.
    
      - Specify the **User Suffix**, such as *acme.com* for **User
        Principal Name** or *cn=users,dc=acme,dc=com* for
        **Distinguished Name**, in **Base DN**.
        
        <div class="note">
        
        The `ldapsearch(1)` command can be used to get details of your
        LDAP settings. To get details related to a specific user, run:
        
            # ldapsearch -D "cn=directory manager" -H ldap://www.acme.com:389 -b "dc=acme,dc=com" -s sub "(objectclass=*)" -w password | grep -i dbright
        
        To search for your directory server’s distinguished name (DN)
        values, run:
        
            # ldapsearch -D "cn=directory manager" -H ldap://www.acme.com:389 -b "dc=acme,dc=com" -s sub "(objectclass=*)" -w password
        
        </div>
        
        **Example: LDAP Configuration.**
        
        ![LDAP authentication full](LDAP-authentication-full.png)

7.  Configure your **Role Settings**: In both LDAP and LDAPS, you can
    use groups from your directory service to set the role for the
    authenticated LDAP user. The LDAP user must be assigned one of the
    account role groups. See [Assigning {product-title\_short} Account
    Roles Using LDAP Groups](#assigning_account_roles_using_ldap_groups)
    for more information.
    
      - For LDAP users not belonging to a group:
        
          - Select a {product-title\_short} group from the **Default
            Group for Users** list. This default group can be used for
            all LDAP users who use LDAP for authentication only. Do not
            select **Get User Groups from LDAP**, which will hide the
            **Default Group for Users** option.
    
      - For LDAP users belonging to a group:
        
          - Select **Get User Groups from LDAP** to retrieve the user’s
            group membership from LDAP. This looks up all groups in the
            directory server for the user attempting to log in. This
            group list is matched against the available groups
            configured in {product-title\_short}. Once a match is found,
            the role associated with the matching group identifies the
            authority the user will have on {product-title\_short}. This
            requires group names on the directory server to match
            {product-title\_short} group names. Selecting this box
            enables user records to be automatically created in
            {product-title\_short} when a user logs in.
            
            <div class="important">
            
            If you do not select **Get User Groups from LDAP**, the user
            must be defined in the VMDB where the User ID is the same as
            the user’s name in your directory service typed in
            lowercase. See [Creating a
            User](https://access.redhat.com/documentation/en-us/red_hat_cloudforms/4.7/html-single/general_configuration/#creating_a_user)
            in *General Configuration* for steps on creating users.
            
            </div>
            
            <div class="note">
            
            If your LDAP directory uses the `groupMembership` attribute
            to contain a user’s group membership, you can use a
            multi-value attribute to look up a user’s groups in
            {product-title\_short}. This is not the default
            {product-title\_short} behaviour, and must be enabled
            manually in the advanced settings. After configuring your
            LDAP settings, update the default {product-title\_short}
            LDAP configuration to support `groupMembership` in
            menu:Configuration\[Settings \> Advanced\] by changing
            `group_attribute: memberof` to `:group_attribute:
            groupmembership`.
            
            </div>
        
          - Select **Get Groups from Home Forest** to use the LDAP
            groups from the LDAP user’s home forest. This will allow you
            to discover groups on your directory server and create
            {product-title\_short} groups based on your directory
            server’s group names. Any user logging in will be assigned
            to that group. This option is only displayed when **Get User
            Groups from LDAP** is selected.
            
            <div class="note">
            
            In most environments, it is recommended to select both the
            **Get User Groups from LDAP** and **Get Groups from Home
            Forest** options.
            
            </div>
        
          - Select **Follow Referrals** to look up and bind a user that
            exists in a domain other than the one configured in the LDAP
            authentication settings.
        
          - Specify the user name to bind to the directory server in
            **Bind DN**. This user must have read access to all users
            and groups that will be used for {product-title\_short}
            authentication and role assignment, for example, a service
            account user with access to all LDAP users (named *svc-ldap*
            in this example).
        
          - Enter the password for the Bind DN user in **Bind
            Password**.

8.  Click **Validate** to verify your settings.

9.  Click **Save**.

LDAP authentication is now configured in your CloudForms environment.

To use a multi-value attribute to look up LDAP group membership, update
the `group_attribute` field in the {product-title\_short} advanced
settings. In menu:Configuration\[Settings \> Advanced\], change
`group_attribute: memberof` to `:group_attribute: groupmembership`.

To assign account roles using LDAP groups, see [Assigning
{product-title\_short} Account Roles Using LDAP
Groups](#assigning_account_roles_using_ldap_groups).

# Adding Trusted Forests

Optionally, if a user has group memberships in another LDAP forest,
specify the settings to access the memberships in the trusted forest.

When trusted forests are added to the authentication configuration, they
are used only for finding groups that a user is a member of.
{product-title\_short} will first collect all of the user’s groups from
the primary LDAP directory. Then it will collect any additional groups
that the user is a member of from all of the configured forests.

The collected LDAP groups are used to match, by name, against the groups
defined in {product-title\_short}. The user must be a member of at least
one matching LDAP group to be successfully authenticated.

To add another trusted forest:

1.  Click ![config gear](config-gear.png) (**Configuration**).

2.  Select your server in the **Settings** accordion.

3.  Select the **Authentication** tab.

4.  Select **Get User Groups from LDAP**, and enter all items in the
    **Role Settings** area.

5.  In the **Trusted Forest Settings** area, click ![green
    plus](green-plus.png)(**Click to add a new forest**).

6.  Enter the **LDAP Host Name**, select a **Mode**, and enter an **LDAP
    Port**, **Base DN**, **Bind DN**, and **Bind Password**.

7.  Click **Save**.

After adding other trusted LDAP forests, you can then change the order
in which {product-title\_short} looks up the forests for authentication.
For instructions, see [Configuring Lookup Priority for LDAP
Groups](#ldap_lookup_priority).

# Assigning {product-title\_short} Account Roles Using LDAP Groups

After configuring LDAP authentication as described in
[article\_title](#ldap_settings), you can associate
{product-title\_short} account roles with your LDAP users. The LDAP
directory server defines the groups and users for
{product-title\_short}, while {product-title\_short} defines the account
roles, and maps the roles to the privileges the LDAP user has.

There are two ways to associate your LDAP groups with
{product-title\_short} account roles:

  - Create groups in {product-title\_short} that match your existing
    LDAP groups by name, and assign the groups account roles; or

  - Create groups on your directory server based on the default account
    roles in {product-title\_short}.

The users in your LDAP groups then inherit the {product-title\_short}
account roles for the LDAP group(s) they are in.

The authentication process then happens as such:

1.  *LDAPuser1* attempts to log into {product-title\_short}, so
    {product-title\_short} queries the directory server to verify it
    knows *LDAPuser1*.

2.  The directory server then confirms that it knows *LDAPuser1*, and
    provides information about the LDAP groups *LDAPuser1* belongs to:
    *Group1*.

3.  {product-title\_short} then looks up *Group1*, and discovers that
    *Group1* is associated with *Role1*.

4.  {product-title\_short} then associates *LDAPuser1* with *Group1* in
    {product-title\_short}, and then allows the user to perform tasks
    allowable by that role.

## Mapping Existing LDAP Groups to {product-title\_short} User Account Roles

This section provides instructions for mapping your existing LDAP groups
to account roles in {product-title\_short}. As a result, the users in
the LDAP group will then be assigned to the {product-title\_short} roles
associated with that group.

1.  Click ![config gear](config-gear.png) (**Configuration**).

2.  Click the **Access Control** accordion, then click **Groups**.

3.  Click ![1847](1847.png) (**Configuration**), and ![plus
    green](plus_green.png) (**Add a new Group**) to create a group.

4.  There are two ways to specify the group to use:
    
      - In the **Description** field, enter the common name (*cn*) for
        your existing LDAP group assigned to users requiring access to
        {product-title\_short}.
    
      - Select **Look Up LDAP Groups** to find a list of groups assigned
        to a specific user in LDAP, then use the **LDAP Group for User**
        list to choose a group.
        
        1.  In **User to Look Up**, enter the common name (*cn*) for a
            user in your LDAP group.
        
        2.  Enter the **Username**.
        
        3.  In **Password**, enter the user’s password. Click
            **Retrieve**.

5.  Select a **Role** to map to the group.

6.  Select a **Project/Tenant** to map to the group.
    
    ![Assign LDAP Roles](Assign_LDAP-Roles.png)

7.  Select any filters to apply to what this group can view in the
    **Assign Filters** area:
    
    1.  In the **My Company Tags** tab, select tags to limit the user to
        items containing those tags. The items that have changed show in
        a blue italicized font.
    
    2.  In the **Host & Clusters** tab, select the host and clusters to
        limit the user to. The items that have changed show in a blue
        italicized font. ![2093](2093.png)
    
    3.  In the **VMs & Templates** tab, select the folders created in
        your virtual infrastructure to limit the user to. The items that
        have changed show in a blue italicized font.

8.  Click **Add**.

To configure the LDAP group lookup priority, see [Configuring Lookup
Priority for LDAP Groups](#ldap_lookup_priority).

## Creating LDAP Groups Based on {product-title\_short} Account Roles

You can also configure access control for LDAP users by creating groups
on your directory server based on {product-title\_short} user account
roles.

Your LDAP group names must match the account role names in
{product-title\_short}. The LDAP users in that group are then
automatically assigned to that specific account role.

In your LDAP directory service:

1.  Define a distribution group for one or more of the account roles
    with the names shown in the table below. This group must be in the
    LDAP directory source you specified for the server. See
    [article\_title](#ldap_settings).
    
    | Directory Service Distribution Group Name | Account Role               |
    | ----------------------------------------- | -------------------------- |
    | EvmGroup-administrator                    | Administrator              |
    | EvmGroup-approver                         | Approver                   |
    | EvmGroup-auditor                          | Auditor                    |
    | EvmGroup-consumption\_administrator       | Consumption Administrator  |
    | EvmGroup-container\_administrator         | Container Administrator    |
    | EvmGroup-container\_operator              | Container Operator         |
    | EvmGroup-desktop                          | Desktop                    |
    | EvmGroup-operator                         | Operator                   |
    | EvmGroup-security                         | Security                   |
    | EvmGroup-super\_administrator             | Super Administrator        |
    | EvmGroup-support                          | Support                    |
    | EvmRole-tenant\_administrator             | Tenant Administrator       |
    | EvmRole-tenant\_quota\_administrator      | Tenant Quota Administrator |
    | EvmGroup-user                             | User                       |
    | EvmGroup-user\_limited\_self\_service     | User Limited Self Service  |
    | EvmGroup-user\_self\_service              | User Self Service          |
    | EvmGroup-vm\_user                         | VM User                    |
    

    Account Role and Directory Service Group Names

2.  Assign each user of your directory service that you want to have
    access to {product-title\_short} membership to one of these groups.

On your {product-title\_short} appliance:

1.  Click ![config gear](config-gear.png) (**Configuration**).

2.  Click the **Settings** accordion, then select your server under
    **Zones**.

3.  Click the **Authentication** tab and enable **Get User Groups from
    LDAP** after typing in all of the required LDAP authentication
    settings. See [article\_title](#ldap_settings).

# Configuring Lookup Priority for LDAP Groups

{product-title\_short} can have multiple LDAP groups configured, which
the appliance will attempt to authenticate with one by one until it
succeeds. The lookup priority of these groups can be rearranged.

<div class="note">

On initial login, a user’s *current group* assignment is the highest
priority group. User group membership, on subsequent logins, is set as
the last assigned group from the prior session.

</div>

To configure the order in which {product-title\_short} looks up LDAP
groups:

1.  Click ![config gear](config-gear.png) (**Configuration**).

2.  Click on the **Access Control** accordion, then click **Groups**.

3.  Click ![1847](1847.png) (**Configuration**), and ![plus
    green](plus_green.png) (**Edit Sequence of User Groups for LDAP Look
    Up**) to prioritize which group a user will default to if LDAP
    returns multiple matching groups.

4.  Select one or more consecutive groups and use the arrow buttons to
    move the user group higher or lower in priority.

5.  Click **Save**.

# Testing LDAP Configuration

To test that your LDAP or LDAPS group configuration is working correctly
with {product-title\_short}:

1.  Log out of the {product-title\_short} user interface.

2.  Log back in as an LDAP user that is assigned to one or more of the
    matching groups.

3.  Change groups by clicking on the user dropdown menu on the top right
    of the user interface. The dropdown list will show the groups the
    user is authorized for.

You can also check the logs in `/var/www/miq/vmdb/log/audit.log` or
`/var/www/miq/vmdb/log/evm.log` to verify your LDAP configuration is
working correctly with the following steps:

1.  Run the following command in a terminal to view the log messages in
    real time:
    
        $ tail -f /var/www/miq/vmdb/log/audit.log

2.  Log into the CloudForms user interface as an LDAP user, while
    checking `/var/www/miq/vmdb/log/audit.log` for updated status,
    success, or failure messages. Alternatively, you can test your LDAP
    configuration by viewing the logs in `/var/www/miq/vmdb/log/evm.log`
    with `grep`, which are more verbose.

# Troubleshooting LDAP Configuration

To test a problematic {product-title\_short} LDAP configuration, run the
following command to see if the user been pulled from LDAP with the
right group. For example:

    # ldapsearch -x -H ldap://ldap-example:389 -LLL \ -b "ou=people,dc=example,dc=com" -s sub \ -D "ui=:userid,ou=People,dc=example,dc=com" -w :password \ "(objectclass=organizationalPerson)

To test if the user belongs to right group, include one of the following
lines in the `ldapsearch` command above:

    (&(objectClass=user)(sAMAccountName=yourUserName) (memberof=CN=YourGroup,OU=Users,DC=YourDomain,DC=com))

or

    -b "ou=groups, dc=example,dc=com"
