RFC that is basis of authz: https://datatracker.ietf.org/doc/html/rfc2904

## Data level entitlements:

Good artcles:


https://enterprise-knowledge.com/inside-the-unified-entitlements-architecture/#:~:text=modify%20queries%20in%2Dflight%20to%20add%20entitlement%2Daware%20filters

Typical Interaction Flow (UML Sequence Pattern)
User/application initiates data access request.

The application authenticates (via OAuth2/SAML) and sends the request with user identity and attributes.

Entitlement Integration Core looks up roles/permissions for the unified user.

Policy Engine evaluates requested action against current policies.

Query Federation Layer rewrites/modifies data query to restrict results to entitled data.

The system retrieves filtered data and logs the access decision with context for auditing.

Systems (databases, data lakes, etc.) provide just the subset of data aligned to granted entitlements.​
