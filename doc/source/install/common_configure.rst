2. Edit the ``/etc/octopus/octopus.conf`` file and complete the following
   actions:

   * In the ``[database]`` section, configure database access:

     .. code-block:: ini

        [database]
        ...
        connection = mysql+pymysql://octopus:OCTOPUS_DBPASS@controller/octopus
