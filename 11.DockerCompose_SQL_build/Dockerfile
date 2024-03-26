# Use the MSSQL Server image as the base image
FROM  mcr.microsoft.com/mssql/server
USER root
# Create a directory for the data files with permissions for a user group
RUN mkdir /var/opt/sqlserver \
    && chown root:mssql /var/opt/sqlserver \
    && chmod 770 /var/opt/sqlserver

# Start the SQL Server service
CMD ["/opt/mssql/bin/sqlservr"]
