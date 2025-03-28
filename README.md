# CPRE416Assignment2Question2
This is my solution to question 2 of assignment 2 from CPRE 416 at ISU


Question:
1. (5 points) Write a minimal Java class AppCache that uses Singleton to store and retrieve cached data,
ensuring exactly one instance can exist. Show how you enforce the Singleton (e.g., private constructor,
getInstance() method). The cached data is Map<EnhancementId, ConfigurationData> which forms
a mapping from each EnhancementId to its ConfigurationData.
2. (5 points) Demonstrate, via a short code snippet, how other parts of the application might use
AppCache to add/update cached data via: set(EnhancementId enhancementId, ConfigurationData
configurationData) or retrieve cached data via get(EnhancementId enhancementId).
3. (5 points) Briey discuss at least one performance or memory concern that can arise when storing too
much in a global cache. If your application is multi-threaded, how might you ensure thread safety?

Answer:
1. See AppCache. The singleton is enforced with "private static final AppCache INSTANCE = new AppCache();"  and "private AppCache()".  The declaration ensures that the INSTANCE belongs to the class and not a specific object and it cannot be reassigned or accessed from t outside of the class.
2. See CacheUser.
3. We may run into an OutOfMemory because of too many writes to a global cache without freeing data.  The thread safety issue is fixed by the use of a concurrent hash map; which allows for atomic operation without locking the entire map for every operation on it.  You could also use a synchronized wrapper Collections.synchronizedMap(new HashMap<>()), but this would add the liitation that only 1 thread can act on the map at a time.
