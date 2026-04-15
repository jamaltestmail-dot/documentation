====================
Timesheets assistant
====================

The timesheet assistant monitors computer and browser activities using
`ActivityWatch <https://activitywatch.net/>`_ to generate timesheet entry suggestions and simplify
timesheet logging.

To use it,
:ref:`activate the feature <timesheets/timesheets-assistant/activation>` and :ref:`install the
ActivityWatch app <timesheets/timesheets-assistant/install-desktop>` on the computer, along with the
:ref:`browser extension <timesheets/timesheets-assistant/install-browser>` if browser activity
tracking is required.

Suggestions are generated based on :ref:`assistant rules <timesheets/timesheets-assistant/assistant-rules>`,
calendar events and planning in Odoo, then matched to projects and tasks, taking into account
previously matched suggestions. They can then be
:ref:`reviewed and converted into timesheet entries <timesheets/timesheets-assistant/use>` directly
from the timesheet assistant view.

.. important::
   The user’s activity data is processed locally on their device and is never shared with anyone,
   either within or outside their organization. Not even Odoo, as a company, can access a user’s
   activity.

.. _timesheets/timesheets-assistant/configuration:

Configuration
=============

 .. _timesheets/timesheets-assistant/activation:

Activation
----------

.. important::
   The timesheet assistant is only available when the :guilabel:`Encoding method` is set to
   :guilabel:`Hours / Minutes` in the :guilabel:`Timesheets Settings`.

To enable the timesheet assistant, go to
:menuselection:`Timesheets --> Configuration --> Settings --> Timesheets` and enable
:guilabel:`Timesheets Assistant`.

Installation
------------

The timesheet assistant tracks user activity through the
`ActivityWatch <https://activitywatch.net/>`_ app
(for :ref:`computer activity <timesheets/timesheets-assistant/install-desktop>`) and browser
extension (for :ref:`browser activity <timesheets/timesheets-assistant/install-browser>`). To
install the timesheet assistant, follow these steps:

#. Go to :menuselection:`Timesheet --> Assistant`.

#. If the browser displays a popup requesting permission to access apps and devices on your device,
   click :guilabel:`Allow`.
#. Follow the installation steps for
   :ref:`Desktop activity <timesheets/timesheets-assistant/install-desktop>` (mandatory) and
   :ref:`Browser activity <timesheets/timesheets-assistant/install-browser>` (optional).

.. tip::
   If the popup does not appear in Google Chrome, follow these steps:

   #. Click the tune icon (:guilabel:`View site information`) to the left of the address bar.
   #. Click :guilabel:`Site settings`.
   #. At the bottom of the :guilabel:`Permissions` list, set the :guilabel:`Apps on device` field to
      :guilabel:`Allow`.
   #. Refresh the Odoo Timesheets page.

   To grant this permission in Mozilla Firefox, refer to the `Mozilla documentation
   <https://support.mozilla.org/en-US/kb/control-personal-device-local-network-permissions-firefox>`_.

.. seealso::
   `ActivityWatch documentation <https://docs.activitywatch.net/en/latest/>`_

 .. _timesheets/timesheets-assistant/install-desktop:

Desktop activity
~~~~~~~~~~~~~~~~

To track time spent in applications on your computer, install the ActivityWatch application by
going to :menuselection:`Timesheets --> Assistant`, clicking :guilabel:`Start Now`, and following
the instructions for your operating system below.

.. note::
   The minimum supported versions are Windows 10, macOS 10.15, and Ubuntu 22, or later.

.. tabs::

   .. tab:: Windows

      #. In the :guilabel:`Install Timesheets Assistant` window, click :guilabel:`Download
         for Windows` in the :guilabel:`Desktop Activity` section, then select your OS version.

        .. note::
           The `Windows installation package can also be downloaded directly
           <https://nightly.odoo.com/aw/windows/activitywatch-odoo_patched-latest-setup.exe>`_.

      #. Install the package and follow the instructions.
      #. Once the installation is finished, restart your computer or log out and log back in.
      #. Access the Odoo database, go to :menuselection:`Timesheets --> Assistant`, and click
         :guilabel:`Start Now`.
      #. Click :guilabel:`Next` twice.
      #. In the :guilabel:`Configure CORS` window, copy the Odoo database URL.
      #. Click :guilabel:`Open Settings`.
      #. On the ActivityWatch web page, scroll down to the :guilabel:`Server Settings` section and
         paste the Odoo database URL in the :guilabel:`CORS` field.
      #. Click :guilabel:`Next` twice.
      #. Click :guilabel:`Test connection` to verify the connection between the Odoo database and
         the ActivityWatch server.

   .. tab:: Mac

      #. `Download the ActivityWatch package for macOS <https://github.com/ActivityWatch/activitywatch/releases/download/v0.13.2/activitywatch-v0.13.2-macos-x86_64.dmg>`_.
      #. Open the downloaded `.dmg` file and move the ActivityWatch app into your
         :guilabel:`Applications` folder.
      #. Launch ActivityWatch.
      #. Click the ActivityWatch icon in the menu bar, select :guilabel:`Modules Menu`, and
         enable one of the following options:

         - :guilabel:`Python Server (aw-server)` (default server)
         - :guilabel:`Rust Server (aw-server-rust)` (more efficient server)

      #. Click the ActivityWatch icon in the menu bar and select :guilabel:`Open Configuration
         Folder.`
      #. Configure the server based on the option selected earlier.

         **Python server configuration**

         #. In the :guilabel:`activitywatch` folder, open the :guilabel:`aw-server` folder, then
            the :file:`aw-server.toml` file.
         #. In the `[server]` section, update the `#cors_origins` parameter with your Odoo database
            URL, without a trailing slash:

            .. code-block:: toml

               [server]
               #host = "localhost"
               #port = "5600"
               #storage = "peewee"
               #cors_origins = "https://your-odoo-database-url.com"

         #. Leave the remaining parameters unchanged and save the file.

         **Rust server configuration**

         #. In the :guilabel:`activitywatch` folder, open the :guilabel:`aw-server-rust` folder,
            then the :file:`config.toml` file.
         #. In the `DEFAULT SETTINGS` section, update the `#cors` parameter with your Odoo database
            URL, without a trailing slash:

            .. code-block:: toml

               ### DEFAULT SETTINGS ###
               #address = "127.0.0.1"
               #port = 5600
               #cors = ["https://your-odoo-database-url.com"]
               #
               #[custom_static]

         #. Leave the remaining parameters unchanged and save the file.

      #. Restart the ActivityWatch app.

   .. tab:: Linux

      #. In the :guilabel:`Install Timesheets Assistant` window, click :guilabel:`Download for
         Linux` in the :guilabel:`Desktop Activity` section, then select your OS version.

        .. note::
           The `Linux installation package can also be downloaded directly
           <https://nightly.odoo.com/aw/ubuntu/activitywatch-odoo.deb>`_.

      #. Install the package and follow the instructions.
      #. Once the installation is finished, restart your computer or log out and log back in.
      #. Access the Odoo database, go to :menuselection:`Timesheets --> Assistant`, and click
         :guilabel:`Start Now`.
      #. Click :guilabel:`Next` twice.
      #. In the :guilabel:`Configure CORS` window, copy the Odoo database URL.
      #. Click :guilabel:`Open Settings`.
      #. On the ActivityWatch web page, scroll down to the :guilabel:`Server Settings` section and
         paste the Odoo database URL in the :guilabel:`CORS` field.
      #. Click :guilabel:`Next`.
      #. Click the Odoo icon in your system tray (usually in the top bar or bottom right of your
         screen), then click :guilabel:`Start Server` or :guilabel:`Restart Server`.
      #. Click :guilabel:`Next` twice.
      #. Click :guilabel:`Test connection` to verify the connection between the Odoo database and
         the ActivityWatch server.

.. note::

   Optionally, ActivityWatch also provides
   `a wide range of watchers <https://docs.activitywatch.net/en/latest/watchers.html>`_ dedicated to
   specific activities that can be installed manually. Using more activity watchers allows the
   timesheet assistant to provide more accurate results.

 .. _timesheets/timesheets-assistant/install-browser:

Browser activity
~~~~~~~~~~~~~~~~

Optionally, install the ActivityWatch browser extension to track time spent in browser tabs and
websites.

To install ActivityWatch browser extensions from Odoo, follow these steps:

#. Go to :menuselection:`Timesheets --> Assistant`.
#. Click the :icon:`fa-cog` (:guilabel:`Settings`) icon in the right part of the screen and select
   :guilabel:`Install Assistant`.
#. In the :guilabel:`Install Timesheets Assistant` window, click the Firefox or Chrome extension
   button  in the :guilabel:`Browser activity` section, depending on your browser.
#. Click :guilabel:`Add to Chrome`, then :guilabel:`Add extension` for Chrome, or
   :guilabel:`Add to Firefox`, then :guilabel:`Add` for Firefox.

.. note::
   ActivityWatch browser extensions are only available for Google Chrome and Mozilla Firefox. The
   `Firefox <https://addons.mozilla.org/en-US/firefox/addon/aw-watcher-web/>`_ and
   `Chrome <https://chromewebstore.google.com/detail/activitywatch-web-watcher/nglaklhklhcoonedhgnpgddginnjdadi>`_
   extensions can also be installed from their respective store pages.

 .. _timesheets/timesheets-assistant/assistant-rules:

Assistant rules
---------------

Assistant rules use regular expressions (regex) to define how Odoo interprets desktop and browser
activity and converts it into timesheet entry suggestions.

These rules act as *key events*: once a key event is triggered, any subsequent activity of at least
one minute is associated with that event until a new key event is triggered by a matching rule.
Preconfigured rules are available to track time spent in Odoo, GitHub, Google Docs, Gmail, Google
Meet, and Discord.

.. tip::

   - Regex can be powerful but complex. `RegexOne <https://regexone.com/>`_ provides interactive
     exercises to help learn it.
   - Adding more rules improves the precision of timesheet suggestions and reduces the impact of
     short or irrelevant entries.

To create or edit an assistant rule, go to :menuselection:`Timesheets --> Configuration -->
Assistant Rules`, then click :guilabel:`New` or select an existing rule, and fill in or edit the
fields described below. Once done, click :guilabel:`Save`.

- :guilabel:`Name`: The name of the rule.

- :guilabel:`Regex`: The pattern matched against ActivityWatch events (window name, tab name or URL)
  to identify and classify activities as key events and display them in the timesheet assistant.

- :guilabel:`Type`: Determines the icon displayed for matching entries in the
  :guilabel:`Suggestions` list of the timesheet assistant.

- :guilabel:`Template`: Defines the name of the generated timesheet entry and is used by
  :ref:`local rules <timesheets/timesheets-assistant/local-rules>` for further processing. If left
  blank, the rule's :guilabel:`Name` is used instead.

- :guilabel:`Description`: A display-only label shown in the Timesheet Assistant. It is purely
  indicative and has no impact on local rules or timesheet generation.

- :guilabel:`Always active`: When enabled, activities matched by this rule are tracked even if
  ActivityWatch marks the user as inactive after three minutes of keyboard and mouse inactivity.
  This is useful for rules covering activities such as meetings.

   .. tip::
      To set a default project and task for timesheet entries created from matching activities,
      click the :icon:`oi-settings-adjust` (:guilabel:`additional options`) button in the list
      header, enable :guilabel:`Project` and :guilabel:`Task`, then select the desired values from
      the fields in the list view.

.. example::

   Here's an example for a Google Meet rule. When ActivityWatch recognizes a Google Meet video
   conference using these regex parameters, the timesheets assistant makes it a key event.

   - :guilabel:`Name`: Customer Meeting
   - :guilabel:`Regex`: `meet - (.*)\|https://meet.google.com`
   - :guilabel:`Type`: Video Conference
   - :guilabel:`Template`: Customer Meeting ($1) (refers to the value captured by the first group in
     the regex)
   - :guilabel:`Description`: Customer Meeting
   - :guilabel:`Project` and :guilabel:`Task`: Left empty, since each meeting may belong to a
     different customer/task
   - :guilabel:`Always active`: Enabled

 .. _timesheets/timesheets-assistant/local-rules:

.. tip::

   :guilabel:`Local Assistant Rules` show the project and task assigned to each ActivityWatch key
   event. It is available for informational purposes, to help understand why Odoo selects a project
   or task for a key event, or why Odoo does not detect the correct project or task.

   When suggested timesheet entries are matched with projects, Odoo learns from those selections to
   improve future suggestions. The data shown here indicate how timesheet entry patterns are
   analyzed to help recommend relevant projects and tasks based on past behavior.

   To view the list of key events detected by ActivityWatch and the project and task assigned to
   them based on the configured :ref:`assistant rules
   <timesheets/timesheets-assistant/assistant-rules>` and/or the project and task assigned to past
   suggested timesheet entries, activate :ref:`developer mode <developer-mode>`, then go to
   :menuselection:`Timesheets --> Configuration --> Local Assistant Rules`.

 .. _timesheets/timesheets-assistant/use:

Use Timesheets Assistant
========================

Once the timesheet assistant has been :ref:`configured
<timesheets/timesheets-assistant/configuration>`, computer and browser (if
:ref:`applicable <timesheets/timesheets-assistant/install-browser>`) activities are
automatically tracked at startup each day, and calendar events and planning in Odoo are checked.
Timesheet entry suggestions are then generated from
:ref:`key events <timesheets/timesheets-assistant/assistant-rules>` detected by ActivityWatch based
on tracked activities when their duration exceeds one minute.

To view the suggestions, go to :menuselection:`Timesheets --> Assistant`. By default,
:guilabel:`Suggestions` are listed :guilabel:`By Project`; click
:guilabel:`Chronological` in the top-right of the panel to switch to chronological order.

To create a timesheet entry from one or multiple suggestions, click the relevant suggestion(s) in
the list, :ref:`edit the fields <timesheets/timesheets/log-manually>` in the left pane if necessary,
and click :guilabel:`Create`.

To delete a suggestion, hover over it and click :guilabel:`Remove`. To delete multiple suggestions
at once, select them in the list and click :guilabel:`Delete`.

To edit or delete an existing timesheet entry, click it in the left pane, make the necessary
changes, then click :guilabel:`Save` or click :guilabel:`Delete`.

.. note::

   - The :guilabel:`Time Rounding` settings apply to timesheet suggestions.
   - Three minutes or more without mouse or keyboard activity are interpreted as inactivity (i.e.,
     a break), unless the :guilabel:`Always Active` option is enabled for a matching
     :ref:`rule <timesheets/timesheets-assistant/assistant-rules>`.
   - Timesheet suggestions are automatically assigned to projects and tasks based on the configured
     :ref:`assistant rules <timesheets/timesheets-assistant/assistant-rules>` and the project and
     task assigned to past suggestions in the timesheet assistant.
   - Timesheet suggestions remain private until timesheet entries are created from them.

.. tip::

   To view the data recorded by ActivityWatch, activate :ref:`developer mode <developer-mode>`, go
   to :menuselection:`Timesheets --> Assistant`, and click :guilabel:`View ActivityWatch Data` at
   the bottom of the suggestions list.
