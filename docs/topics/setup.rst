Setup
=====

The Firefox Marketplace is a collection of services and repositories that
together form the Marketplace.

Our recommended setup for the backend is to use :ref:`Docker <backend>`. And our
recommended setup for the frontend is to clone the repository as detailed
in our :ref:`frontend` documentation. By default, the frontend setup will point
to our development server and database. But if you wanted a full environment,
you can set up both the backend and frontend, and point your frontend towards
the backend set up by Docker.


Setting up the Marketplace Backend
----------------------------------

If you want to work on the backend, the API, or the payments infrastructure,
visit our :ref:`backend` documentation. It will explain how to set up Docker as
it automates the setup of the Marketplace environment.


Setting up the Marketplace Frontend
-----------------------------------

If you want to work on the consumer-facing Marketplace frontend, visit our
:ref:`frontend` documentation. It only takes three commands to get things
up and running. You don't even need to setup a backend, although you could
if you wanted your own personal playground.


List of Services and Repositories
---------------------------------

Backend
~~~~~~~

* **Zamboni**: the main API backend that also serves developer, reviewer, and admin tool pages.
  Written in Python with Django -
  `source <https://github.com/mozilla/zamboni>`_,
  `docs <https://zamboni.readthedocs.org>`_,
  `API docs <https://firefox-marketplace-api.readthedocs.org>`_.

* **Marketplace API Mock**: a fake API backend used for frontend testing.
  Written in Python with Flask -
  `source <https://github.com/mozilla/marketplace-api-mock>`_.

* **Monolith**: storage and query server for statistics around the Marketplace.
  Written in Python -
  `source <https://github.com/mozilla/monolith-client>`_,
  `aggregator source <https://github.com/mozilla/monolith-aggregator/>`_.

* **Webpay** and **Solitude**: servers for processing payments for the Marketplace.
  Written in Python with Django -
  `webpay source <https://github.com/mozilla/solitude/>`_,
  `webpay docs <https://webpay.readthedocs.org>`_,
  `solitude source <https://github.com/mozilla/webpay/>`_,
  `solitude docs <https://solitude.readthedocs.org>`_.

* **Trunion**: a signing service for app receipts and packaged apps.
  Written in Python with Pyramid -
  `source <https://github.com/mozilla/trunion/>`_.

* **Zippy**: a fake backend for payments so to fake out carrier billing.
  Written in Node -
  `source <https://github.com/mozilla/zippy>`_.

* **APK Factory**: generates Android APKs out of web apps.
  Written in Node and Python -
  `factory source <https://github.com/mozilla/apk-factory-service/>`_,
  `signer source <https://github.com/mozilla/apk-signer>`_,
  `signer docs <http://apk-signer.readthedocs.org/>`_.

* **marketplace-env**: automated Marketplace backend setup using Docker.
  Uses Docker and fig -
  `source <https://github.com/mozilla/marketplace-env>`_

Frontend (Javascript)
~~~~~~~~~~~~~~~~~~~~~

* **Fireplace**: the main frontend for the Firefox Marketplace.
  Written in Javascript with our Commonplace framework -
  `source <https://github.com/mozilla/fireplace>`_.

* **Statistics**: dashboard that displays charts and graphs from Monolith.
  Written in Javascript with our Commonplace framework -
  `source <https://github.com/mozilla/marketplace-stats/>`_.

* **Transonic**: curation and editorial tools for the Marketplace, notably for the Feed.
  Written in Javascript with our Commonplace framework -
  `source <https://github.com/mozilla/transonic/>`_.

* **Operator Dashboard**: dashboard for FirefoxOS operators to manage their app collections.
  Written in Javascript with our Commonplace framework -
  `source <https://github.com/mozilla/commbadge/>`_.

* **Commbadge**: dashboard for communications between app reviewers and app developers.
  Written in Javascript with our Commonplace framework -
  `source <https://github.com/mozilla/commbadge/>`_.

* **Spartacus**: the frontend for Webpay.
  Written in Javascript -
  `source <https://github.com/mozilla/spartacus>`_.

Frontend Components (Javascript)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* **marketplace-core-modules**: core JS modules for Marketplace frontend projects
  Written in Javascript -
  `source <https://github.com/mozilla/marketplace-core-modules>`_.

* **commonplace**: Node module that includes configuration, template optimization, l10n.
  Written in Node -
  `source <https://github.com/mozilla/commonplace>`_.

* **marketplace-gulp**: gulpfiles for Marketplace frontend projects for builds.
  Written in Node -
  `source <https://github.com/mozilla/marketplace-gulp>`_.

* **marketplace-constants**: shared constants between the backend and frontend.
  Written in Python -
  `source <https://github.com/mozilla/marketplace-constants>`_.

Serving With Nginx
~~~~~~~~~~~~~~~~~~

Marketplace is designed to be an app accessible at one domain, hitting Nginx.

Behind the scenes Nginx will proxy to the other servers on your behalf.

Most developers are using Nginx to serve out the multiple services. Your
configuration may look something like this:

.. image:: ../img/configuration.png

You can find an example configuration file in
`our Docker repository <https://github.com/mozilla/marketplace-env/blob/master/images/nginx/nginx.conf>`_.

Default Ports
~~~~~~~~~~~~~

By default, the services listen to the following ports:

+---------------------+--------+
| Project             | Port   |
+=====================+========+
| Zamboni             | 2600   |
+---------------------+--------+
| Webpay              | 2601   |
+---------------------+--------+
| Solitude            | 2602   |
+---------------------+--------+
| Solitude Proxy      | 2603   |
+---------------------+--------+
| Spartacus           | 2604   |
+---------------------+--------+
| Zippy               | 2605   |
+---------------------+--------+
| Fireplace           | 8675   |
+---------------------+--------+
| Commbadge           | 8676   |
+---------------------+--------+
| Statistics          | 8677   |
+---------------------+--------+
| Transonic           | 8678   |
+---------------------+--------+
| Operator Dashboard  | 8679   |
+---------------------+--------+
