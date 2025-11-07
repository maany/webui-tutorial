## 📚 Additional Resources

- **Style Guide**: [Design System Documentation](https://rounded-clave-f1d.notion.site/Rucio-WebUI-Design-System-2a15a7432d01802e8a45e6fb0e1af26f?source=copy_link)
- **Dependency Injection**: Inversify documentation - https://inversify.io/
- **Streaming**: NDJSON specification - http://ndjson.org/
- **Testing**: Jest documentation - https://jestjs.io/


---

## 📌 Tutorial Example Files

This tutorial uses the `list-subscriptions` feature as a complete example. All the backend infrastructure (Gateway, UseCase, Controller, Presenter) exists in the production codebase. For the frontend components, we've created tutorial-specific example files:

**Tutorial Example Components** (created for this tutorial):
- `src/component-library/pages/Subscriptions/list/ListSubscriptionTutorialExample.tsx` - Main page component
- `src/component-library/pages/Subscriptions/list/ListSubscriptionTutorialTable.tsx` - Table component

---

**Production Components** (actual implementation):
- `src/component-library/pages/Subscriptions/list/ListSubscription.tsx` - Uses `list-subscription-rule-states` endpoint
- `src/component-library/pages/Subscriptions/list/ListSubscriptionTable.tsx` - Displays aggregated rule state counts

---

The tutorial example components demonstrate the `list-subscriptions` feature that returns individual subscription records, while the production components use a different feature that returns aggregated subscription rule state counts. Both are valid examples of the Clean Architecture pattern described in this tutorial.

**Questions?** Shoot a message on Mattermost or check existing implementations code for examples!
