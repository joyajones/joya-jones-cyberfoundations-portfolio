# Week 7 Notes — Cloud Heights: The Guard Post

**Student Name:** Joya Jones

**Week:** 7

## Firewall and Security Group

```text
A firewall controls network traffic by applying rules that allow or deny connections. In Azure, Network Security Groups (NSGs) use security rules to control inbound and outbound traffic.

“A network security rule is a decision about traffic.”
```

## Rule Anatomy

```text
(priority, direction, source, destination, protocol, port, action)
```

## First Match Wins

```text
Firewall rules are evaluated in priority order, beginning with the lowest number. Once traffic matches a rule, the firewall applies its action and stops evaluating further rules.

“Inbound and outbound traffic use separate ledgers.”
```

## Least Privilege

```text
Least privilege means granting only the access necessary for a specific purpose. Narrow firewall rules limit access to the required source, destination, protocol, and port instead of allowing unnecessary traffic.
```

## Testing and Evidence

```text
Configuring a security rule doesn't prove that it works as intended. Connection tests provide evidence of actual network behavior. Testing both an authorized and unauthorized source helps verify that intended traffic is allowed while other traffic is restricted.

“A configured service, a security rule, a test result, and an evidence screenshot answer different questions.”
```

## Troubleshooting and Remediation

```text
Troubleshooting should follow a logical process based on how the system is supposed to function. Check the VM, service, rule configuration, and evaluation order before changing anything. Identify the cause, make a targeted correction, and retest to verify that the issue is resolved.

“Create a controlled priority failure inside your student range, diagnose it from evidence, remove the problem, and retest.”
```

## Questions I Still Have

```text
How can I get more hands-on experience diagnosing firewall and network security issues in real-world environments?
```
