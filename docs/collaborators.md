# Managing collaborator access

!!! abstract

    The OSDF currently uses [COmanage](https://incommon.org/software/comanage/) 
    for managing access to authenticated namespaces.

    In this guide, you'll learn

    * how to login to the COmanage registry
    * how to find the groups controlling your namespace
    * how to give collaborators access to your namespace

This guide is intended for users who manage a custom namespace in the OSDF,
usually set up in coordination with the OSDF team.
If you were not directed to this page by a member of the OSDF team,
the following instructions likely do not apply to you.

For assistance, consider emailing the OSDF team at <a href="mailto:support@osg-htc.org">support@osg-htc.org</a>.

## Login to COmanage

This section covers how to login to COmanage.
These instructions assume that you have registered your identity with COmanage previously,
which should be the case if you are the manager of a custom namespace.

1. Go to [registry.cilogon.org](https://registry.cilogon.org).

    ![Login page for COmanage Registry](assets/comanage-registry-login.png)

2. Click on the "LOGIN" button.

3. On the CILogon page, select the appropriate identity provider and click "Log On".
    Typically, this is the same identity provider you used when you first registered in COmanage.

    !!! tip
    
        We recommend that you do not click the "Remember this selection" box until after you've
        done several successful authentications. It can be tricky to "undo" this box, so it is
        best to make sure everything is working first!

    ![Login to CILogon in browser](/assets/osdf-upload-cilogon.png)

4. Sign in to your selected identity provider as you normally would.

You may be automatically logged in, depending on your browser settings.

You should see the following page once you've successfully logged in:

![Home page for COmanage Registry](assets/comanage-registry-home.png)

## Your namespace and COmanage groups

To see the COmanage groups that you manage:

1. Open the left-side navigation menu.
2. Click on the "Groups" dropdown.
3. Click on the "My Groups" link in the dropdown.
4. In the filter bar at the top of the group list, click on filter "Groups I'm a member of" to remove it (and only show "Groups I manage").

Alternatively, [use this link](https://registry.cilogon.org/registry/co_groups/index/co:7/search.owner:1/op:search) to get to the same page.

## Add collaborators to your namespace


