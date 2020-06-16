.. _iface-images:

******
Images
******

==================
 Image interface
==================

::
   
   template <int dimensions = 1,
             typename AllocatorT = cl::sycl::image_allocator>
   class image;

.. rubric:: Template parameters

| ``dimensions`` -
| ``AllocatorT`` -

.. rubric:: Member functions
	    
========================  ==========
:ref:`image-image`
get_range_
get_pitch_
get_count_
get_size_
get_allocator_
get_access_
set_final_data_
set_write_back_
========================  ==========

.. _image-image:

(constructors)
==============

::
   
  image(image_channel_order order, image_channel_type type,
        const range<dimensions> &range, const property_list &propList = {});

::
   
  image(image_channel_order order, image_channel_type type,
        const range<dimensions> &range, AllocatorT allocator,
        const property_list &propList = {});

.. parsed-literal::
   
  image(image_channel_order order, image_channel_type type,                 [#dimgtr1]_
        const range<dimensions> &range, const range<dimensions - 1> &pitch,
        const property_list &propList = {});

.. parsed-literal::
   
  image(image_channel_order order, image_channel_type type,                 [#dimgtr1]_
        const range<dimensions> &range, const range<dimensions - 1> &pitch,
        AllocatorT allocator, const property_list &propList = {});

::
   
  image(void *hostPointer, image_channel_order order,
        image_channel_type type, const range<dimensions> &range,
        const property_list &propList = {});

::
   
  image(void *hostPointer, image_channel_order order,
        image_channel_type type, const range<dimensions> &range,
        AllocatorT allocator, const property_list &propList = {});

::
   
  image(const void *hostPointer, image_channel_order order,
        image_channel_type type, const range<dimensions> &range,
        const property_list &propList = {});

::
   
  image(const void *hostPointer, image_channel_order order,
        image_channel_type type, const range<dimensions> &range,
        AllocatorT allocator, const property_list &propList = {});

.. parsed-literal::
   
  image(void \*hostPointer, image_channel_order order,                       [#dimgtr1]_
        image_channel_type type, const range<dimensions> &range,
        range<dimensions - 1> &pitch, const property_list &propList = {});   

.. parsed-literal::
   
  image(void \*hostPointer, image_channel_order order,                       [#dimgtr1]_
        image_channel_type type, const range<dimensions> &range,
        range<dimensions - 1> &pitch, AllocatorT allocator,
        const property_list &propList = {});

::
   
  image(shared_ptr_class<void> &hostPointer, image_channel_order order,
        image_channel_type type, const range<dimensions> &range,
        const property_list &propList = {});

::
   
  image(shared_ptr_class<void> &hostPointer, image_channel_order order,
        image_channel_type type, const range<dimensions> &range,
        AllocatorT allocator, const property_list &propList = {});

.. parsed-literal::
   
  image(shared_ptr_class<void> &hostPointer, image_channel_order order,     [#dimgtr1]_
        image_channel_type type, const range<dimensions> &range,
        const range<dimensions - 1> &pitch, const property_list &propList = {});

.. parsed-literal::
   
  image(shared_ptr_class<void> &hostPointer, image_channel_order order,     [#dimgtr1]_
        image_channel_type type, const range<dimensions> &range,
        const range<dimensions - 1> &pitch, AllocatorT allocator,
        const property_list &propList = {});

::
   
  image(cl_mem clMemObject, const context &syclContext,
        event availableEvent = {});

.. [#dimgtr1] Available only when: dimensions > 1

.. rubric:: Parameters

| ``order`` -
| ``type`` -
| ``range`` -
| ``propList`` - See `Image properties`_
| ``allocator`` -
| ``pitch`` -
| ``hostPointer`` -
| ``syclContext`` -
| ``clMemObject`` -
| ``availableEvent`` -

get_range
=========

::
   
  range<dimensions> get_range() const;

.. rubric:: Returns

get_pitch
=========

::
   
  range<dimensions-1> get_pitch() const;

Available only when dimensions > 1

.. rubric:: Returns

get_count
=========

::

  size_t get_count() const;

.. rubric:: Returns

get_size
========

::

  size_t get_size() const;

.. rubric:: Returns

get_allocator
=============

::

  AllocatorT get_allocator() const;

.. rubric:: Returns

get_access
==========

::

  template <typename dataT, access::mode accessMode>
  accessor<dataT, dimensions, accessMode, access::target::image>
  get_access(handler & commandGroupHandler);

::

  template <typename dataT, access::mode accessMode>
  accessor<dataT, dimensions, accessMode, access::target::host_image>
  get_access();

.. rubric:: Template parameters

| ``dataT`` -
| ``accessMode`` -

.. rubric:: Parameters

| ``commandGroupHandler`` -

.. rubric:: Returns
	    
set_final_data
==============

::

  template <typename Destination = std::nullptr_t>
  void set_final_data(Destination finalData = nullptr);

Description

.. rubric:: Template parameters

| ``Destination`` -

.. rubric:: Parameters

| ``finalData`` -


set_write_back
==============

::

  void set_write_back(bool flag = true);

.. rubric:: Parameters

| ``flag`` -

==================
 Image properties
==================

===================================  ======
`property::image::use_host_ptr`_
`property::image::use_mutex`_
`property::image::context_bound`_
===================================  ======

property::image::use_host_ptr
==============================

::

   class property::image::use_host_ptr;

Description

.. rubric:: Member functions

======================================  =======
:ref:`image-use_host_ptr-use_host_ptr`
======================================  =======

.. _image-use_host_ptr-use_host_ptr:

(constructors)
--------------

::

   use_host_ptr();

Description

property::image::use_mutex
==========================

::

   class property::image::use_mutex;

Description

.. rubric:: Member functions

========================================  =======
:ref:`image-get_mutex_ptr-get_mutex_ptr`
get_mutex_ptr_
========================================  =======
   
.. _image-get_mutex_ptr-get_mutex_ptr:
   
(constructors)
--------------

::

   use_mutex();

Description

get_mutex_ptr
-------------

::

   mutex_class *get_mutex_ptr() const;


Description

property::image::context_bound
==============================


::

   property::image::context_bound;

Description

.. rubric:: Member functions

========================================  =======
:ref:`image-context_bound-context_bound`
get_context_
========================================  =======

.. _image-context_bound-context_bound:

(constructors)
--------------

::

   use_mutex();


Description


get_context
-----------

::

   context get_context() const;


Description

.. rubric:: Returns
	    
===================
Image_channel_order
===================

::
   
   enum class image_channel_order : unsigned int {
     a,
     r,
     rx,
     rg,
     rgx,
     ra,
     rgb,
     rgbx,
     rgba,
     argb,
     bgra,
     intensity,
     luminance,
     abgr
   }

==================
Image_channel_type
==================

::
   
   enum class image_channel_type : unsigned int {
     snorm_int8,
     snorm_int16,
     unorm_int8,
     unorm_int16,
     unorm_short_565,
     unorm_short_555,
     unorm_int_101010,
     signed_int8,
     signed_int16,
     signed_int32,
     unsigned_int8,
     unsigned_int16,
     unsigned_int32,
     fp16,
     fp32
   }