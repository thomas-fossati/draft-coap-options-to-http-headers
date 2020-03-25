the idea (AFAIU) is to project coap options into http headers so that their
semantics is understood by http entities and can be acted upon.  the use case
from which this originates is the "hop count" header in the dots signalling
protocol that is lost when crossing an http "hop" and would otherwise provide
useful info to forwarding nodes that need to detect loops in the topology.

the document's scope seems to be:

define a generic framework for encoding coap options into http headers which is
sema-conserving -- it has to be usable by on-path http entities, not just
safely tunneled across http links.  creating a generic translation framework
should simplify the life of future spec writers that need to define
interoperable metadata semantics across http and coap.  the idea is to have a
procedure in place to automatically derive an http header from the
corresponding coap option.

note that the framework can be immediately tested on the "hop count" use case,
which should be specified by this document.

question: do we need to cater for other use cases?  for example:
* are we interested in having a generic way to allow sending http endpoints to
  be able to encode coap options for the destination endpoint when going
  through a H2C proxy?
    * can that be avoided in the first place?
    * and in any case, what are the security implications?

* translation rules to/from coap

* what to do with unknown non-critical options?

* procedures for registering HTTP headers (e.g., provide a template in line
  with https://tools.ietf.org/html/rfc7231#section-8.3.1)

* option structure, things to encode:
  * meta (needed?)
    * criticality
    * proxy safety
    * cacheability
    * repeatability
  * further meta
    * format (how to encode opaque?)
    * length constraints
    * default type
  * data
    * the HTTP friendly encoding of the option value
