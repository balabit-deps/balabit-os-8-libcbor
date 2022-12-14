Type 7 – Floats & control tokens
=================================

This type combines two completely unrelated types of items -- floating point numbers and special values such as true, false, null, etc. We refer to these special values as 'control values' or 'ctrls' for short throughout the code.

Just like integers, they have different possible width (resulting in different value ranges and precisions).

.. doxygenenum:: cbor_float_width

==================================  =========================================
Corresponding :type:`cbor_type`     ``CBOR_TYPE_FLOAT_CTRL``
Number of allocations               One per lifetime
Storage requirements                ``sizeof(cbor_item_t) + 1/4/8``
==================================  =========================================

Getting metadata
~~~~~~~~~~~~~~~~~

.. doxygenfunction:: cbor_float_ctrl_is_ctrl
.. doxygenfunction:: cbor_float_get_width
.. doxygenfunction:: cbor_ctrl_is_bool

Reading data
~~~~~~~~~~~~~

.. doxygenfunction:: cbor_float_get_float2
.. doxygenfunction:: cbor_float_get_float4
.. doxygenfunction:: cbor_float_get_float8
.. doxygenfunction:: cbor_float_get_float
.. doxygenfunction:: cbor_ctrl_value

Creating new items
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygenfunction:: cbor_new_ctrl
.. doxygenfunction:: cbor_new_float2
.. doxygenfunction:: cbor_new_float4
.. doxygenfunction:: cbor_new_float8
.. doxygenfunction:: cbor_new_null
.. doxygenfunction:: cbor_new_undef


Building items
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygenfunction:: cbor_build_bool
.. doxygenfunction:: cbor_build_ctrl
.. doxygenfunction:: cbor_build_float2
.. doxygenfunction:: cbor_build_float4
.. doxygenfunction:: cbor_build_float8


Manipulating existing items
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. doxygenfunction:: cbor_set_ctrl
.. doxygenfunction:: cbor_set_float2
.. doxygenfunction:: cbor_set_float4
.. doxygenfunction:: cbor_set_float8


.. _api_type_7_hard_floats:

Half floats
~~~~~~~~~~~~
CBOR supports two `bytes wide ("half-precision") <https://en.wikipedia.org/wiki/Half-precision_floating-point_format>`_
floats which are not supported by the C language. *libcbor* represents them using `float <https://en.cppreference.com/w/c/language/type>` values throughout the API, which has important implications when manipulating these values.

In particular, if a user uses some of the manipulation APIs
(e.g. :func:`cbor_set_float2`, :func:`cbor_new_float2`)
to introduce a value that doesn't have an exect half-float representation,
the encoding semantics are given by :func:`cbor_encode_half` as follows:

.. doxygenfunction:: cbor_encode_half
