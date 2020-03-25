## Scope

The idea (AFAIU) is to project CoAP options into HTTP headers so that their
semantics is understood by HTTP entities and can be acted upon.  The use case
from which this originates is the "hop count" header in the DOTS signalling
protocol that is lost when crossing an HTTP "hop" and would otherwise provide
useful info to forwarding nodes that need to detect loops in the topology.

The document's scope seems to be the definition of a generic framework for
encoding CoAP options into HTTP headers that is sema-conserving -- it has to be
usable by on-path HTTP entities, not just safely tunneled across HTTP links.
Creating a generic translation framework should simplify the life of future
spec writers that need to define interoperable metadata semantics across HTTP
and CoAP.  The idea is to have a procedure in place to (semi-)automatically
derive an HTTP header from the corresponding CoAP option.

Note that the framework can be immediately tested on the "hop count" use case,
which should be specified by this document.

## Misc Notes

* Do we need to cater for other use cases?  For example:
  * Are we interested in having a generic way to allow sending HTTP endpoints
    to be able to encode CoAP options for the destination endpoint when going
    through a H2C proxy?
    * Can that be avoided in the first place?
    * And in any case, what are the security implications?

* Define translation rules to/from CoAP
  * Should we use [header structure](https://tools.ietf.org/html/draft-ietf-httpbis-header-structure)?

* What to do with unknown non-critical options?

* Procedures for registering HTTP headers (e.g., provide a template in line
  with [RFC7231](https://tools.ietf.org/html/rfc7231#section-8.3.1)

* Option structure, things to encode:
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

