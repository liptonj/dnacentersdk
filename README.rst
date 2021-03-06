=============
dnacentersdk
=============

*Work with the DNA Center APIs in native Python!*

-------------------------------------------------------------------------------

**dnacentersdk** is a *community developed* Python library for working with the DNA Center APIs.  Our goal is to make working with DNA Center in Python a *native* and *natural* experience!

.. code-block:: python

    from dnacentersdk import api

    # Create a DNACenterAPI connection object;
    # it uses DNA Center sandbox URL, username and password, with DNA Center API version 1.2.10.
    dnac = api.DNACenterAPI(username="devnetuser",
                            password="Cisco123!",
                            base_url="https://sandboxdnac2.cisco.com:443",
                            version='1.2.10')

    # Find all devices that have 'Switches and Hubs' in their family
    devices = dnac.devices.get_device_list(family='Switches and Hubs')

    # Print all of demo devices
    for device in devices.response:
        print('{:20s}{}'.format(device.hostname, device.upTime))

    # Find all tags
    all_tags = dnac.tag.get_tag(sort_by='name', order='des')
    demo_tags = [tag for tag in all_tags.response if 'Demo' in tag.name ]

    #  Delete all of the demo tags
    for tag in demo_tags:
        dnac.tag.delete_tag(tag.id)
    
    # Create a new demo tag
    demo_tag = dnac.tag.create_tag(name='dna Demo')
    task_demo_tag = dnac.task.get_task_by_id(task_id=demo_tag.response.taskId)

    if not task_demo_tag.response.isError:
        # Retrieve created tag
        created_tag = dnac.tag.get_tag(name='dna Demo')

        # Update tag
        update_tag = dnac.tag.update_tag(id=created_tag.response[0].id, 
                                         name='Updated ' + created_tag.response[0].name,
                                         description='DNA demo tag')
        
        print(dnac.task.get_task_by_id(task_id=update_tag.response.taskId).response.progress)
        
        # Retrieved updated
        updated_tag = dnac.tag.get_tag(name='Updated dna Demo')
        print(updated_tag)
    else:
        # Get task error details 
        print('Unfortunately ', task_demo_tag.response.progress)
        print('Reason: ', task_demo_tag.response.failureReason)


Introduction_


Installation
------------

Installing and upgrading dnacentersdk is easy:

**Install via PIP**

.. code-block:: bash

    $ pip install dnacentersdk

**Upgrading to the latest Version**

.. code-block:: bash

    $ pip install dnacentersdk --upgrade


Documentation
-------------

**Excellent documentation is now available at:**
https://dnacentersdk.readthedocs.io

Check out the Quickstart_ to dive in and begin using dnacentersdk.


Release Notes
-------------

Please see the releases_ page for release notes on the incremental functionality and bug fixes incorporated into the published releases.


Questions, Support & Discussion
-------------------------------

dnacentersdk is a *community developed* and *community supported* project.  If you experience any issues using this package, please report them using the issues_ page.


Contribution
------------

dnacentersdk_ is a community development projects.  Feedback, thoughts, ideas, and code contributions are welcome!  Please see the `Contributing`_ guide for more information.


Inspiration
------------

This library is inspired by the webexteamssdk_  library


*Copyright (c) 2019 Cisco and/or its affiliates.*

.. _Introduction: https://dnacentersdk.readthedocs.io/en/latest/api/intro.html
.. _dnacentersdk.readthedocs.io: https://dnacentersdk.readthedocs.io
.. _Quickstart: https://dnacentersdk.readthedocs.io/en/latest/api/quickstart.html
.. _dnacentersdk: https://github.com/cisco-en-programmability/dnacentersdk
.. _issues: https://github.com/cisco-en-programmability/dnacentersdk/issues
.. _pull requests: https://github.com/cisco-en-programmability/dnacentersdk/pulls
.. _releases: https://github.com/cisco-en-programmability/dnacentersdk/releases
.. _the repository: dnacentersdk_
.. _pull request: `pull requests`_
.. _Contributing: https://github.com/cisco-en-programmability/dnacentersdk/blob/master/docs/contributing.rst
.. _webexteamssdk: https://github.com/CiscoDevNet/webexteamssdk

