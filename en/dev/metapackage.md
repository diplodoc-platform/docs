# Metapackage

A metapackage is one of the ways to simplify modular development of projects.

The development process in a metapackage is somewhat different from the more popular approach of a "monorepository".

The key difference is that each module inside a metapackage contains independent infrastructure.
The metapackage itself only adds an additional layer of infrastructure to improve the development experience in a modular system.

A monorepo, in contrast, has shared infrastructure. Modules inside a monorepo cannot be built outside of it. 