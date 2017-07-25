Prerequisites
-------------

Before you install and configure the service service,
you must create a database, service credentials, and API endpoints.

#. To create the database, complete these steps:

   * Use the database access client to connect to the database
     server as the ``root`` user:

     .. code-block:: console

        $ mysql -u root -p

   * Create the ``octopus`` database:

     .. code-block:: none

        CREATE DATABASE octopus;

   * Grant proper access to the ``octopus`` database:

     .. code-block:: none

        GRANT ALL PRIVILEGES ON octopus.* TO 'octopus'@'localhost' \
          IDENTIFIED BY 'OCTOPUS_DBPASS';
        GRANT ALL PRIVILEGES ON octopus.* TO 'octopus'@'%' \
          IDENTIFIED BY 'OCTOPUS_DBPASS';

     Replace ``OCTOPUS_DBPASS`` with a suitable password.

   * Exit the database access client.

     .. code-block:: none

        exit;

#. Source the ``admin`` credentials to gain access to
   admin-only CLI commands:

   .. code-block:: console

      $ . admin-openrc

#. To create the service credentials, complete these steps:

   * Create the ``octopus`` user:

     .. code-block:: console

        $ openstack user create --domain default --password-prompt octopus

   * Add the ``admin`` role to the ``octopus`` user:

     .. code-block:: console

        $ openstack role add --project service --user octopus admin

   * Create the octopus service entities:

     .. code-block:: console

        $ openstack service create --name octopus --description "service" service

#. Create the service service API endpoints:

   .. code-block:: console

      $ openstack endpoint create --region RegionOne \
        service public http://controller:XXXX/vY/%\(tenant_id\)s
      $ openstack endpoint create --region RegionOne \
        service internal http://controller:XXXX/vY/%\(tenant_id\)s
      $ openstack endpoint create --region RegionOne \
        service admin http://controller:XXXX/vY/%\(tenant_id\)s
