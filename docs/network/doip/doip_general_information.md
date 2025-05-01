# Doip general information

DoIP is defined in ISO 13400

## Terms and definitions
- DoIP - Diagnostics over Internet Protocol
- diagnostic power mode - abstract vehicle internal power supply state (Not Ready, Ready(all servers accessible via DoIP can communicate), Not Supported etc)
- DoIP edge node - host inside the vehicle, where activation line is terminated and where the link from the first node/host in the external network is terminated
- host - node connected to the IP-based network
- network node - device connected to the IP - based network but does not implement the DoIP protocol
- vehicle sub-network - network not directly connected to the IP-based network

## Symbols and abbreviated terms

## Scope

Mandatory features:
- vehicle network integration (IP address assignment)
- vehicle announcement and vehicle discovery
- vehicle basic status information retrieval
- connection establishment, connection maintenance and vehicle gateway control
- data routing to and from the vehicle's sub-components
- error handling

Optional features:
- DoIP entity status monitoring
- transport layer security
- DoIP entity firewall capabilities

## DoIP introduction

- Started with the introduction of the first legislated emissions-related diagnostics.
- It evolved to optimized data link layer and transport protocol developments in order to make the new in-vehicle networks usable for diagnostic communication.