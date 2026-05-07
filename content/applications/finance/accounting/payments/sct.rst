==========================
SEPA Credit Transfer (SCT)
==========================

.. |sdd| replace:: :abbr:`SCT (SEPA Credit Transfer)`

.. _accounting/sct/sepa-countries:

**SEPA (Single Euro Payments Area)** is a payment-integration initiative of the European Union that
facilitates standardized and simplified electronic payments in euros across SEPA countries. |sdd|
are initiated by the sender (contrary to :doc:`batch_sdd`), and are usually instant or completed
within one business day.

.. note::
   - `List of all SEPA countries
     <https://www.europeanpaymentscouncil.eu/document-library/other/epc-list-sepa-scheme-countries>`_.
   - If your company is located in the EFTA region, a non-EEA SEPA country, or a non-EEA SEPA
     territory, consult the :ref:`ISO20022 <accounting/sct/iso20022>` section.

.. seealso::
   - :doc:`batch_sdd`
   - :doc:`customer_vendor_bank_accounts`

.. _accounting/sct/configuration:

Configuration
=============

Activate |sdd|
--------------

To pay suppliers with |sdd|, you must activate the **SEPA Credit Transfer** setting. To do so, go to
:menuselection:`Accounting --> Configuration --> Settings --> Vendor Payments: SEPA Credit Transfer
(SCT)`. By activating the setting and filling out your company data, you will be able to use the
|sdd| option when paying your vendor.

.. note::
   According to the localization package installed, the **SEPA Direct Debit** and **SEPA Credit
   Transfer** modules may be installed by default. If not, they need to be
   :ref:`installed <general/install>`.

Activate |sdd| methods on banks
-------------------------------

From the **Accounting** app, navigate to :menuselection:`Configuration --> Journals` and open your
:guilabel:`Bank` journal. Click the :guilabel:`Outgoing Payments` tab, and, if not already present,
add :guilabel:`SEPA Credit Transfer` under :guilabel:`Payment Method`.

Finally, specify the :guilabel:`Account Number` and the :guilabel:`Bank` in the :guilabel:`Journal
Entries` tab.

Registering payments
--------------------

To register vendor payments made with |sdd|, first verify that an :guilabel:`Account Number` and
:guilabel:`Bank` are indicated on the vendor's :doc:`contact form <../../../essentials/contacts>`,
under the :guilabel:`Accounting` tab. Odoo automatically verifies if the IBAN format is respected.

Then, go to :menuselection:`Vendors --> Payments`, and click :guilabel:`New`. When creating your
payment, select :guilabel:`SEPA Credit Transfer` as the :guilabel:`Payment Method`. The
:guilabel:`Vendor Bank Account` is automatically populated based on the :guilabel:`Vendor` selected.
For future payments to this vendor, Odoo will automatically suggest you the bank account, but it
remains possible to select a new one from the dropdown menu by clicking the :guilabel:`Vendor Bank
Account` field.

Once your payment is registered, do not forget to confirm it. You can also pay vendor bills from the
bill directly using the :guilabel:`Register Payment` button at the top of a vendor bill. The form is
the same, but the payment is directly linked to the bill and will be automatically reconciled with
it.

.. _accounting/sct/iso20022:

ISO20022
========

ISO 20022 is a global standard for the exchange of payment data between banks. It uses a format that
lets payment details and related documents move together as a single package. This means information
such as invoice numbers, tax details, and who sent the payment is stored in fields that computers
can automatically read.

There are different versions of ISO 20022, called `pain` (e.g., `pain.001.001.009`). These versions
can change over time, and sometimes country-specific versions include extra fields.

Difference with |sdd|
---------------------

|sdd| payments are a use case of ISO 20022, limited to the EUR currency and :ref:`selected list of
countries <accounting/sct/sepa-countries>`, which distinguishes them from the global ISO 20022
standard.

Payments labeled as ‘SEPA’ in Odoo effectively use the global ISO 20022 format, and are therefore
not restricted to EUR or specific countries. This may require additional setup for SEPA compliance
in :ref:`certain regions <accounting/sct/sepa-countries>`.

To enable country-specific SEPA pain versions, check that you have the :doc:`fiscal localization
<../../../finance/fiscal_localizations>` for your country installed in your database. In the
**Accounting** app, go to :menuselection:`Configuration --> Journals`, open your :guilabel:`Bank`
journal, click the :guilabel:`Outgoing` payments tab, and select your country’s :guilabel:`SEPA Pain
Version`.

.. important::
   ISO20022 `pain.001.001.03` is being deprecated in November, 2026. If you need to use ISO20022 as
   a format for e-Invoicing, use `pain.001.001.09`.
