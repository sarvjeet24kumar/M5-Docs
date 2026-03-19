---
hide:
  - toc
---
# TDD - Test Driven Development

## Tools for TDD

- **pytest**: Testing framework.
- **pytest-django**: Django integration for pytest.
- **pytest-mocker**: Mocking functions in tests.
- **pytest-cov**: Generating coverage reports.
- **factory-boy & faker**: Generating realistic test data.

## Example Test Case

We use `factory-boy` to generate consistent test data and `pytest-django` for seamless integration.

```python
@patch("accounts.views.authentication_views.login_otp_service.verify", return_value=(True, None))
    def test_verify_login_success(self, mock_otp_verify, api_client, user, tenant, faker):
        url = reverse("verify-login")
        otp = faker.bothify(text="######")
        response = api_client.post(url, {"username": user.username, "otp": otp}, HTTP_TENANT_ID=str(tenant.id))
        assert response.status_code == status.HTTP_200_OK
        assert "access" in response.data
```

## Executing Test Cases

To run the full test suite efficiently:

```bash
# Run all tests
uv run pytest

# Run a specific module
uv run pytest tests/unit/books/

# Run tests matching a keyword
uv run pytest -k "checkout"
```

## Coverage & Quality

We use `pytest-cov` to track our progress towards full test coverage.

### Terminal Summary
```bash
uv run pytest --cov=.
```

### Detailed HTML Report
```bash
uv run pytest --cov=. --cov-report=html
```

## Report 

<iframe src="../assets/index.html" width="100%" height="1500px"></iframe>
