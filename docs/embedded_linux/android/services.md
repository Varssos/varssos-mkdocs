# Services

[Services overview](https://developer.android.com/develop/background-work/services)


## [Create a bound service](https://developer.android.com/develop/background-work/services/bound-services#Creating)
There are 3 ways to allow client to interace with a bound service:

- `Extend the Binder class`
- `Use a Messenger`
- `Use AIDL`

## [Manage the lifecycle of a bound service](https://developer.android.com/develop/background-work/services/bound-services#Lifecycle)

When a service is unbound from all clients, the Android system destroys it(unless it was started using startService)