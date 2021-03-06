Installation
=============
Installation generally encompasses downloading and generating PyMuPDF and MuPDF from sources. This process consists of three steps described below under :ref:`InstallSource`.

**However**, for popular configurations, binary setups via wheels are available, detailed out under :ref:`InstallBinary`. This process is **much faster**, less error-prone and requires the download of only one 3 MB file (either ``.zip`` or ``.whl``) - no compiler, no Visual Studio, no download of MuPDF, even no download of PyMuPDF.

.. _InstallSource:

Option 1: Install from Sources
-------------------------------

Step 1: Download PyMuPDF
~~~~~~~~~~~~~~~~~~~~~~~~~
Download this repository and unzip / decompress it. This will give you a folder, let us call it ``PyFitz``.

Step 2: Download and Generate MuPDF
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Download ``mupdf-x.xx-source.tar.gz`` from http://mupdf.com/downloads and unzip / decompress it. Call the resulting folder ``mupdf``. The latest MuPDF **development sources** are available on https://github.com/ArtifexSoftware/mupdf - this is **not** what you want here.

Make sure you download the (sub-) version for which PyMuPDF has stated its compatibility. The various Linux flavors usually have their own specific ways to support download of packages which we cannot cover here. Do not hesitate posting issues to our web site or sending an e-mail to the authors for getting support.

Put it inside ``PyFitz`` as a subdirectory for keeping everything in one place.

**Controlling the Binary File Size:**

Since version 1.9, MuPDF includes support for many dozens of additional, so-called NOTO ("no TOFU") fonts for all sorts of alphabets from all over the world like Chinese, Japanese, Corean, Kyrillic, Indonesian, Chinese etc. If you accept MuPDF's standard here, the resulting binary for PyMuPDF will be very big and easily approach or exceed 20 MB. The features actually needed by PyMuPDF in contrast only represent a fraction of this size: no more than 5 MB currently.

To cut off unneeded stuff from your MuPDF version, modify file ``/include/mupdf/config.h`` as follows:
::
 #ifndef FZ_CONFIG_H
 
 #define FZ_CONFIG_H
 
 /*
 Enable the following for spot (and hence overprint/overprint
 simulation) capable rendering. This forces FZ_PLOTTERS_N on.
 */
 #define FZ_ENABLE_SPOT_RENDERING
 
 /*
 Choose which plotters we need.
 By default we build all the plotters in. To avoid building
 plotters in that aren't needed, define the unwanted
 FZ_PLOTTERS_... define to 0.
 */
 /* #define FZ_PLOTTERS_G 1 */
 /* #define FZ_PLOTTERS_RGB 1 */
 /* #define FZ_PLOTTERS_CMYK 1 */
 /* #define FZ_PLOTTERS_N 1 */
 
 /*
 Choose which document agents to include.
 By default all but GPRF are enabled. To avoid building unwanted
 ones, define FZ_ENABLE_... to 0.
 */
 /* #define FZ_ENABLE_PDF 1 */
 /* #define FZ_ENABLE_XPS 1 */
 /* #define FZ_ENABLE_SVG 1 */
 /* #define FZ_ENABLE_CBZ 1 */
 /* #define FZ_ENABLE_IMG 1 */
 /* #define FZ_ENABLE_TIFF 1 */
 /* #define FZ_ENABLE_HTML 1 */
 /* #define FZ_ENABLE_EPUB 1 */
 /* #define FZ_ENABLE_GPRF 1 */
 
 /*
 Choose whether to enable JPEG2000 decoding.
 By default, it is enabled, but due to frequent security
 issues with the third party libraries we support disabling
 it with this flag.
 */
 /* #define FZ_ENABLE_JPX 1 */
 
 /*
 Choose whether to enable JavaScript.
 By default JavaScript is enabled both for mutool and PDF interactivity.
 */
 /* #define FZ_ENABLE_JS 1 */
 
 /*
 Choose which fonts to include.
 By default we include the base 14 PDF fonts,
 DroidSansFallback from Android for CJK, and
 Charis SIL from SIL for epub/html.
 Enable the following defines to AVOID including
 unwanted fonts.
 */
 /* To avoid all noto fonts except CJK, enable: */
 #define TOFU // PyMuPDF
 
 /* To skip the CJK font, enable: (this implicitly enables TOFU_CJK_EXT and TOFU_CJK_LANG) */
 #define TOFU_CJK // PyMuPDF
 
 /* To skip CJK Extension A, enable: (this implicitly enables TOFU_CJK_LANG) */
 #define TOFU_CJK_EXT // PyMuPDF
 
 /* To skip CJK language specific fonts, enable: */
 #define TOFU_CJK_LANG // PyMuPDF
 
 /* To skip the Emoji font, enable: */
 #define TOFU_EMOJI // PyMuPDF
 
 /* To skip the ancient/historic scripts, enable: */
 #define TOFU_HISTORIC // PyMuPDF
 
 /* To skip the symbol font, enable: */
 #define TOFU_SYMBOL // PyMuPDF
 
 /* To skip the SIL fonts, enable: */
 #define TOFU_SIL // PyMuPDF
 
 /* To skip the ICC profiles, enable: */
 #define NO_ICC // PyMuPDF
 
 /* To skip the Base14 fonts, enable: */
 /* #define TOFU_BASE14 */
 /* (You probably really don't want to do that except for measurement purposes!) */
 
 /* ---------- DO NOT EDIT ANYTHING UNDER THIS LINE ---------- */
 
 ... ... ...
 
 #endif /* FZ_CONFIG_H */


The above choice should bring down your binary file size to around 5 MB or less, depending on your bitness.

**Generate MuPDF now**.

The MuPDF source includes generation procedures / makefiles for numerous platforms. For Windows platforms, Visual Studio solution and project definitions are provided.

Consult additional installation hints on PyMuPDF's `main page <https://github.com/rk700/PyMuPDF/>`_ on Github. Among other things you will find a Wiki pages with details on building the Windows binaries or user provided installation experiences.

Step 3: Build / Setup PyMuPDF
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Adjust the setup.py script as necessary. E.g. make sure that
  * the include directory is correctly set in sync with your directory structure
  * the object code libraries are correctly defined

Now perform a ``python setup.py install``.

.. _InstallBinary:

Option 2: Install from Binaries
--------------------------------
This installation option is available for all MS Windows and popular Mac OS and Linux platforms.

Step 1: Install from PyPI
~~~~~~~~~~~~~~~~~~~~~~~~~~
If you find the wheel for your platform on PyPI, issue

``pip install [--upgrade] PyMuPDF``

and **you are done. Continue with next chapter of this manual.**

Step 2: Install from GitHub
~~~~~~~~~~~~~~~~~~~~~~~~~~~
This section applies, if you prefer a ZIP file or if you need a special (bug-fix or pre-release) wheel.

Download your `Windows <https://github.com/JorjMcKie/PyMuPDF-wheels/tree/windows>`_, `Mac OS <https://github.com/JorjMcKie/PyMuPDF-wheels/tree/osx>`_ or `Linux <https://github.com/JorjMcKie/PyMuPDF-wheels/tree/linux>`_ wheel and issue

``pip install [--upgrade] PyMuPDF-<...>.whl``

If your platform is Windows you can also download a `zip file <https://github.com/JorjMcKie/PyMuPDF-Optional-Material/tree/master/binary_setups>`_, unzip it to e.g. your ``Desktop`` and open a command prompt at the unzipped folder's directory, which contains ``setup.py``. Enter ``python setup.py install`` (or ``py setup.py install`` if you have the Python launcher).

MD5 Checksums
~~~~~~~~~~~~~~
Binary download setup scripts in ZIP format contain an integrity check based on MD5 check sums.

The directory structure of each zip file ``pymupdf-<...>.zip`` is as follows:

.. |setup| image:: img-binsetupdirs.png

|setup|

During setup, the MD5 check sum of the four installation files ``__init__.py``, ``_fitz.pyd``, ``utils.py`` and ``fitz.py`` is being calculated and compared against a pre-calculated value in file ``md5.txt``. In case of a mismatch the error message

``md5 mismatch: probable download error``

is issued and setup is cancelled. In this case, please check your download for any problems.

If you downloaded a wheel, integrity checks are done by ``pip``.

Targeting Parallel Python Installations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Setup scripts for ZIP binary install support the Python launcher ``py.exe`` introduced with version 3.3.

They contain **shebang lines** that specify the intended Python version, and additional checks for detecting error situations.

This can be used to target the right Python version if you have several installed in parallel (and of course the Python launcher, too). Use the following statement to set up PyMuPDF correctly:

``py setup.py install``

The shebang line of ``setup.py`` will be interpreted by ``py.exe`` to automatically find the right Python, and the internal checks will make sure that version and bitness are what they sould be.

When using wheels, configuration conflict detection is done by ``pip``.

Using UPX
-------------
No matter which option you chose, your PyMuPDF installation will end up with four files: ``__init__.py``, ``fitz.py``, ``utils.py`` and the binary file ``_fitz<...>.xxx`` in the ``site-packages`` directory. The extension of the binary will be ``.pyd`` on Windows and ``.so`` on other platforms.

Depending on your OS, your compiler and your font support choice (see above), this binary can be quite large and range from 5 MB to 20 MB. You can reduce this by applying the compression utility `UPX <https://upx.github.io/>`_ to it, which probably also exists for your operating system. UPX will reduce the size of ``_fitz<...>.xxx`` by more than 50%. You will end up with 2.5 MB to 9 MB without impacting functionality nor execution speed.
