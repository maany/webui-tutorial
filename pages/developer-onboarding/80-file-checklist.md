## 📋 Quick Reference: File Checklist

When creating a new feature `MyFeature` for listing items:

### Core Layer (Business Logic)
- [ ] `src/lib/core/entity/rucio.ts` - Add entity types if needed
- [ ] `src/lib/core/dto/my-feature-dto.ts` - DTOs
- [ ] `src/lib/core/port/secondary/my-feature-gateway-output-port.ts` - Gateway interface
- [ ] `src/lib/core/port/primary/my-feature-port.ts` - Input/Output ports
- [ ] `src/lib/core/usecase-models/my-feature-usecase-models.ts` - Request/Response/Error models
- [ ] `src/lib/core/use-case/my-feature-usecase.ts` - Use case implementation

### Infrastructure Layer
- [ ] `src/lib/infrastructure/gateway/my-feature-gateway/my-feature-gateway.ts` - Gateway implementation
- [ ] `src/lib/infrastructure/gateway/my-feature-gateway/endpoints/list-my-feature-endpoint.ts` - Endpoint
- [ ] `src/lib/infrastructure/gateway/my-feature-gateway/my-feature-gateway-utils.ts` - Data transformers
- [ ] `src/lib/infrastructure/controller/my-feature-controller.ts` - Controller
- [ ] `src/lib/infrastructure/presenter/my-feature-presenter.ts` - Presenter
- [ ] `src/lib/infrastructure/data/view-model/my-feature.ts` - View model
- [ ] `src/lib/infrastructure/ioc/features/my-feature-feature.ts` - Feature registration

### API & UI
- [ ] `src/app/api/feature/my-feature/route.ts` - API route
- [ ] `src/component-library/pages/MyFeature/MyFeature.tsx` - Main page
- [ ] `src/component-library/pages/MyFeature/MyFeatureTable.tsx` - Table

### Tests
- [ ] `test/gateway/my-feature/my-feature-gateway.test.ts` - Gateway tests
