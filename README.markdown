AnnA
====

A in-memory AMQP-inspired messaging system.


Why?
====

Why does the world needs another messaging system?

I don't know if it does or not, but I needed one that integrates better
with a project I'm playing with.

In this project, I don't need persistence at all inside the
messaging system.

The queuing is done on WebServers when they receive the request. They
have access to a database with all the data to validate the request, and
write it to a database-based queue.

Then they send the job using AnnA, that manages pool of workers.

AnnA keeps the job in memory only. If AnnA crashes, she can scan those
database-based queue to pick up the current global view.

Each worker asks for jobs and after receiving one gets to work. When
done, either successfully or with an error, it notifies AnnA and update
the job directly on the queue.

AnnA itself never touches the database.

Secondary goals
===============

I want to model the internals as a AMQP system, but I don't plan to use the
AMQP wire protocol for now.

I will use a protocol that can be parsed with pack()/unpack() combinations.


Author and Copyright
====================

The crazy person in charge is Pedro Melo <melo@simplicidade.org>.

The code is released in the same terms as Perl.
