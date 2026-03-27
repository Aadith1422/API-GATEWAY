#  Lessons Learned & Best Practices for Securing GraphQL APIs

##  Lessons Learned (From Completed Labs)

- **GraphQL exposes more data than intended if not restricted**  
  Hidden fields like `postPassword` were accessible through direct queries.

- **Frontend restrictions are not security controls**  
  Data hidden in UI can still be accessed via backend API.

- **Broken Access Control is a major risk**  
  Queries like `getUser(id)` allowed unauthorized access (IDOR).

- **GraphQL introspection reveals schema details**  
  Attackers can discover hidden queries and sensitive fields.

- **Rate limiting can be bypassed using aliases**  
  Multiple login attempts were executed in a single request.

- **GraphQL endpoints can be vulnerable to CSRF**  
  Accepting `application/x-www-form-urlencoded` enabled attacks via HTML forms.

- **Session-based authentication alone is insufficient**  
  Cookies are automatically sent, enabling CSRF attacks.

---

##  Best Practices for Securing GraphQL APIs

###  1. Enforce Authorization at Resolver Level
- Validate permissions for every query and mutation  
- Never rely on frontend restrictions  

---

###  2. Disable or Restrict Introspection
- Disable in production  
- Prevent attackers from discovering schema  

---

###  3. Prevent IDOR (Broken Object-Level Authorization)
- Validate ownership of requested resources  
- Avoid exposing direct object references  

---

###  4. Implement Strong Rate Limiting
- Apply limits per operation  
- Prevent alias-based brute force  

---

###  5. Implement CSRF Protection
- Use CSRF tokens  
- Enforce SameSite cookies  
- Validate Origin/Referer headers  

---

###  6. Restrict Content Types
- Accept only `application/json`  
- Block unnecessary formats like `x-www-form-urlencoded`  

---

###  7. Limit Query Complexity
- Use query depth limiting  
- Apply query cost analysis  

---

###  8. Protect Sensitive Fields
- Avoid exposing passwords, tokens, secrets  
- Use field-level authorization  

---

###  9. Logging & Monitoring
- Log GraphQL queries  
- Detect abnormal behavior  

---

##  Conclusion

GraphQL is powerful but requires strict security controls.  
Without proper protections, attackers can exploit APIs to:

- Access hidden data  
- Bypass authentication  
- Perform unauthorized actions  

 Secure GraphQL APIs require strong validation, access control, and protection against modern attack techniques.

---

