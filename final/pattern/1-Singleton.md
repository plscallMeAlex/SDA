# Problem
We want only 1 instance of the class in the system to prevent the creation instance and make sure it using the same resource.
# Trade-off
- It easy to access (global)
- Make it hard to governance
# Topology
Having a static attribute that keep the instance.
So after create the first time then next time it need to return  the same instance
# Use-when
- Logger,
- Database connection pool