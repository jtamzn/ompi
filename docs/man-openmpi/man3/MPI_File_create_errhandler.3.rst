.. _mpi_file_create_errhandler:


MPI_File_create_errhandler
==========================

.. include_body

:ref:`MPI_File_create_errhandler` - Creates an MPI-style error handler that
can be attached to a file.


SYNTAX
------


C Syntax
^^^^^^^^

.. code-block:: c

   #include <mpi.h>

   int MPI_File_create_errhandler(MPI_File_errhandler_function *function,
   	MPI_Errhandler *errhandler)


Fortran Syntax
^^^^^^^^^^^^^^

.. code-block:: fortran

   USE MPI
   ! or the older form: INCLUDE 'mpif.h'
   MPI_FILE_CREATE_ERRHANDLER(FUNCTION, ERRHANDLER, IERROR)
   	EXTERNAL	FUNCTION
   	INTEGER	ERRHANDLER, IERROR


Fortran 2008 Syntax
^^^^^^^^^^^^^^^^^^^

.. code-block:: fortran

   USE mpi_f08
   MPI_File_create_errhandler(file_errhandler_fn, errhandler, ierror)
   	PROCEDURE(MPI_File_errhandler_function) :: file_errhandler_fn
   	TYPE(MPI_Errhandler), INTENT(OUT) :: errhandler
   	INTEGER, OPTIONAL, INTENT(OUT) :: ierror


DEPRECATED TYPE NAME NOTE
-------------------------

MPI-2.2 deprecated the MPI_File_errhandler_fn and
MPI::file::Errhandler_fn types in favor of MPI_File_errhandler_function
and MPI::File::Errhandler_function, respectively. Open MPI supports both
names (indeed, the \_fn names are typedefs to the \_function names).


INPUT PARAMETER
---------------
* ``function``: User-defined error handling procedure (function).

OUTPUT PARAMETERS
-----------------
* ``errhandler``: MPI error handler (handle).
* ``IERROR``: Fortran only: Error status (integer).

DESCRIPTION
-----------

Registers the user routine *function* for use as an MPI error handler.
Returns in errhandler a handle to the registered error handler.

In the C language, the user routine *function* should be a C function of
type MPI_File_errhandler_function, which is defined as

::

       typedef void (MPI_File_errhandler_function)(MPI_File *, int *,
       ...);

The first argument to *function* is the file in use. The second is the
error code to be returned by the MPI routine that raised the error.

In the Fortran language, the user routine should be of the form:

.. code-block:: fortran

       SUBROUTINE FILE_ERRHANDLER_FUNCTION(FILE, ERROR_CODE, ...)
           INTEGER FILE, ERROR_CODE


ERRORS
------

.. include:: ./ERRORS.rst
