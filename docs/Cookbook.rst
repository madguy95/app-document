.. _Cookbook:

#########
Cookbook
#########

    This chapter currently focuses on how to copy a work done on the
    eXo Platform server, such as creating navigations, node types and
    templates, to another eXo Platform server throughout these topics:

    -  :ref:`Copying a site's content folder with its version history <PLFDevGuide.Cookbook.CopyingSitesContentFolderWithVersionHistory>`

    -  :ref:`Copying navigation nodes of sites <PLFDevGuide.Cookbook.CopyingNavigationNodesOfSites>`

    -  :ref:`Copying templates of node types <PLFDevGuide.Cookbook.CopyingTemplateOfNodeType>`

    -  :ref:`Copying the Content template <PLFDevGuide.Cookbook.CopyingWCMTemplates>`

    -  :ref:`Copying a category tree <PLFDevGuide.Cookbook.CopyingTaxonomyTree>`

    -  :ref:`Copying metadata templates <PLFDevGuide.Cookbook.CopyingMetadataTemplates>`

    -  :ref:`Copying queries <PLFDevGuide.Cookbook.CopyingQueries>`

    -  :ref:`Copying scripts <PLFDevGuide.Cookbook.CopyingScripts>`

    -  :ref:`Copying drive configurations <PLFDevGuide.Cookbook.CopyingDriveConfigurations>`

    -  :ref:`Copying gadgets <PLFDevGuide.Cookbook.CopyingGadgets>`

    -  :ref:`Restarting the server <PLFDevGuide.Cookbook.RestartingServer>`

The procedure of each step will be detailed as follows:

.. _PLFDevGuide.Cookbook.CopyingSitesContentFolderWithVersionHistory:

==================================================================
Step 1. Copying a site's content folder with its version history
==================================================================

1. Go to the Sites Management drive.

2. Open the site node, for example "acme".

3. Click Export on the Action bar to export the node with its version
   history as below:

	|image0|

4. Select Export and Export Version History to perform the exporting.

5. Navigate to the node where you want to import the file, then click
   Import to open the Import form.

6. Select the exported nodes and version history to be imported.

	|image1|

One pop-up message will appear to inform that you have imported
successfully.

.. _PLFDevGuide.Cookbook.CopyingNavigationNodesOfSites:

==========================================
Step 2. Copying navigation nodes of sites
==========================================

1. Go to the Content Administration page and add a new drive to both 
   target and source servers.

	|image2|

2. Export the navigation node.

	|image3|

3. Import the nodes navigation.

	|image4|

.. _PLFDevGuide.Cookbook.CopyingTemplateOfNodeType:

========================================
Step 3. Copying templates of node types
========================================

1. Add the System drive to both servers.

	|image5|

2. Open ``system:/jcr:system/exo:namespaces/{namespace_name}``, and 
   export it.

	|image6|

3. Open ``system:/jcr:system/exo:namespaces/``, and import the exported
   file as described in :ref:`**Step 2** <PLFDevGuide.Cookbook.CopyingNavigationNodesOfSites>`

	|image7|

4.	Open ``system:/jcr:system/jcr:nodetypes/{node_type}``, and export it.

	|image8|

5. Open ``system:/jcr:system/jcr:nodetypes/``, and import the exported 
   file as described in :ref:`**Step 4** <PLFDevGuide.Cookbook.CopyingWCMTemplates>`.

	|image9|

.. note:: If you have some specific JCR namespaces and node types, you need to import them into the new server.

.. _PLFDevGuide.Cookbook.CopyingWCMTemplates:

=====================================
Step 4. Copying the Content template
=====================================

1. Add the DMS Administration drive to both servers.

   |image10|

.. note:: You need to select dms-system for the Workspace field.

2. Open the DMS Administration drive.

3. Open ``dms-system:/exo:ecm/templates/{node_type}``, and export it.

   |image11|

4. Open ``dms-system:/exo:ecm/templates/``, and import the exported file.

   |image12|

Also, for the CLV templates, you can find all template views defined in
the ``dms-system:/exo:ecm/views`` path with:

-  userviews: this folder contains views of Sites Explorer with a set of
   actions.

-  templates: where you can find all gtmpl templates of:

   -  Category Navigation Portlet templates.

   -  Content List Viewer (CLV) templates and its paginator templates.

   -  ecm-explorer templates define how to display nodes in the Sites
      Explorer portlet, such as Content, List and Thumbnails views.

   -  Search templates is used in the Content Search portlet to define
      the form, layout, result and result's paginator.

If you want to reuse one of the non-predefined templates above, simply
export and import it into the new server at the same place.

.. note:: If you have some specific Content (CLV) views and/or templates of node types, you will need to import them into the new server.

.. _PLFDevGuide.Cookbook.CopyingTaxonomyTree:

=================================
Step 5. Copying a category tree
=================================

By importing the whole site as described in the :ref:`Copying a site's content folder with its version history <PLFDevGuide.Cookbook.CopyingSitesContentFolderWithVersionHistory>`
section, you will also have the category tree imported. The default
location where the site's category is placed in a sub-folder is named
category. So, you do not need to export or import them because this step
is automatically done. But the category tree definition is still not
fully imported in the new server. What you need to do is to add this
category tree definition by following these steps:

1. Open the DMS Administration drive in the new server.

2. Go to ``dms-system:/exo:ecm/exo:taxonomyTrees/definition``.

3. Add a symlink to the Category Tree Root Node, for example
   ``collaboration:/sites/acme``.

   |image13|

The name of symlink is displayed as "acme".

|image14|

The symlink will be generated as below:

|image15|

In some cases, to see changes, you need to clear the cache by
disconnecting or restarting the server.

|image16|

.. _PLFDevGuide.Cookbook.CopyingMetadataTemplates:

===================================
Step 6. Copying metadata templates
===================================

1. Open the DMS Administration drive in the new server.

2. Go to ``/exo:ecm/metadata/{meta_data_name}``.

3. Export and import it in the same location in the new server again.

.. _PLFDevGuide.Cookbook.CopyingQueries:

========================
Step 7. Copying queries
========================

1. Open the DMS Administration drive in the new server.

2. Go to ``/exo:ecm/queries/{query_name}``.

3. Export and import it in the same location in the new server again.

.. _PLFDevGuide.Cookbook.CopyingScripts:

========================
Step 8. Copying scripts
========================

1. Open the DMS Administration drive in the new server.

2. Go to ``/exo:ecm/scripts/ecm-explorer``.

	You will find three folders referring to the three types of groovy
	scripts in eXo Platform, including:

	-  action: The action scripts are launched when an ECM action triggers
	   them. For more information, refer to :ref:`Managing actions <ManagingActions>`.

	-  interceptor: Interceptor scripts are triggered before and/or after
	   the JCR node is saved, or when a node is created or edited. They are
	   used to either validate the value entered in a form or to manipulate
	   the newly created node, for example, to map the new node with a forum
	   thread or any other type of discussion areas.

	-  widget: Widget scripts are used to fill widgets, such as a select box
	   in a dynamic way.

3. Export your customized script in the same location in the new server.

.. _PLFDevGuide.Cookbook.CopyingDriveConfigurations:

======================================
Step 9. Copying drive configurations
======================================

1. Open the DMS Administration drive in the new server.

2. Go to ``/exo:ecm/exo:drives/{drive_name}``.

3. Export and import it in the same location in the new server again.

.. _PLFDevGuide.Cookbook.CopyingGadgets:

=========================
Step 10. Copying gadgets
=========================

1. Open the drive that points into the Portal-System Workspace.

2. Go to your gadget by following the
   ``portal-system:/production/app:gadgets/{gadget_name}`` path.

3. Export and import it in the same location in the new server again.

.. _PLFDevGuide.Cookbook.RestartingServer:

===============================
Step 11. Restarting the server
===============================

After importing the site navigation nodes, the site may look quite
broken, so you need to restart the server first. After the server is
restarted, the site will look like:

|image17|

.. |image0| image:: images/how_to_copy_a_site/export_site_nodes2.png
.. |image1| image:: images/how_to_copy_a_site/import_site_nodes2.png
.. |image2| image:: images/how_to_copy_a_site/add_portal_system_drive.png
.. |image3| image:: images/how_to_copy_a_site/export_site_navigations.png
.. |image4| image:: images/how_to_copy_a_site/import_site_navigations.png
.. |image5| image:: images/how_to_copy_a_site/add_system_drive.png
.. |image6| image:: images/how_to_copy_a_site/export_namespace.png
.. |image7| image:: images/how_to_copy_a_site/import_namespace.png
.. |image8| image:: images/how_to_copy_a_site/export_node_type.png
.. |image9| image:: images/how_to_copy_a_site/import_nodetype.png
.. |image10| image:: images/how_to_copy_a_site/add_dms_admin_drive.png
.. |image11| image:: images/how_to_copy_a_site/export_node_type_templates.png
.. |image12| image:: images/how_to_copy_a_site/import_node_type_templates.png
.. |image13| image:: images/how_to_copy_a_site/select_TaxonomyTree_rootNode.png
.. |image14| image:: images/how_to_copy_a_site/select_TaxonomyTree_rootNode2.png
.. |image15| image:: images/how_to_copy_a_site/select_TaxonomyTree_rootNode3.png
.. |image16| image:: images/how_to_copy_a_site/TaxonomyTree_added_successfully.png
.. |image17| image:: images/how_to_copy_a_site/acme_site_after_import_and_restart.png
