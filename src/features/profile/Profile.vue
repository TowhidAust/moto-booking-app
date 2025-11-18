
<script setup lang="ts">
import { ref, reactive, onMounted } from 'vue'
import Card from '@/components/ui/card/Card.vue'
import CardContent from '@/components/ui/card/CardContent.vue'
import CardHeader from '@/components/ui/card/CardHeader.vue'
import CardTitle from '@/components/ui/card/CardTitle.vue'
import Button from '@/components/ui/button/Button.vue'
import { useRouter } from 'vue-router'

const router = useRouter()

const defaultAvatar = '/src/assets/logo.svg'

const profile = reactive({
	name: 'Towhid Ahmed',
	phone: '+880 1712-345678',
	email: 'towhid@example.com',
	address: '123 Dhanmondi, Dhaka 1209, Bangladesh',
	avatar: defaultAvatar,
})

const avatarFile = ref<File | null>(null)
const avatarPreview = ref<string>(profile.avatar)

const errors = reactive({
	name: '',
	phone: '',
	email: '',
	address: '',
})

const loadProfile = () => {
	
}

onMounted(() => loadProfile())

const saveProfile = () => {

}

const resetProfile = () => {
	loadProfile()
	avatarFile.value = null
}

const goBack = () => router.back()
</script>

<template>
	
		<div>
			<div class="flex items-center justify-between mb-6">
				<h1 class="text-2xl font-bold">My Profile</h1>
				<div class="flex gap-2">
					<Button variant="outline" @click="goBack">Back</Button>
				</div>
			</div>

			<div class="grid grid-cols-1 md:grid-cols-3 gap-6">
				<!-- Avatar and summary -->
				<div>
					<Card class="p-4 text-center">
						<div class="flex flex-col items-center gap-4">
							<div class="w-32 h-32 rounded-full overflow-hidden bg-gray-100 flex items-center justify-center">
								<img :src="avatarPreview" alt="avatar" class="w-full h-full object-cover" />
							</div>
							<label class="text-sm text-gray-600">Upload Avatar</label>
							<input type="file" accept="image/*" class="w-full" />
							<div class="w-full text-left">
								<p class="text-sm text-gray-600">Name</p>
								<p class="font-semibold text-gray-900">{{ profile.name || '—' }}</p>
								<p class="text-sm text-gray-600 mt-2">Phone</p>
								<p class="font-semibold text-gray-900">{{ profile.phone || '—' }}</p>
								<p class="text-sm text-gray-600 mt-2">Email</p>
								<p class="font-semibold text-gray-900">{{ profile.email || '—' }}</p>
							</div>
						</div>
					</Card>
				</div>

				<!-- Editable form -->
				<div class="md:col-span-2">
					<Card>
						<CardHeader>
							<CardTitle>Profile Information</CardTitle>
						</CardHeader>
						<CardContent class="space-y-4">
							<div>
								<label class="text-sm font-medium text-gray-700">Full Name</label>
								<input v-model="profile.name" type="text" class="mt-1 w-full p-3 rounded-lg border" />
								<p v-if="errors.name" class="text-sm text-red-600 mt-1">{{ errors.name }}</p>
							</div>

							<div>
								<label class="text-sm font-medium text-gray-700">Phone</label>
								<input v-model="profile.phone" type="text" class="mt-1 w-full p-3 rounded-lg border" />
								<p v-if="errors.phone" class="text-sm text-red-600 mt-1">{{ errors.phone }}</p>
							</div>

							<div>
								<label class="text-sm font-medium text-gray-700">Email (optional)</label>
								<input v-model="profile.email" type="email" class="mt-1 w-full p-3 rounded-lg border" />
								<p v-if="errors.email" class="text-sm text-red-600 mt-1">{{ errors.email }}</p>
							</div>

							<div>
								<label class="text-sm font-medium text-gray-700">Address</label>
								<textarea v-model="profile.address" rows="3" class="mt-1 w-full p-3 rounded-lg border"></textarea>
								<p v-if="errors.address" class="text-sm text-red-600 mt-1">{{ errors.address }}</p>
							</div>

							<div class="flex gap-3 pt-2">
								<Button variant="default" @click="saveProfile">Save Profile</Button>
								<Button variant="outline" @click="resetProfile">Reset</Button>
							</div>
						</CardContent>
					</Card>
				</div>
			</div>
		</div>
</template>

<style scoped>
.rounded-full img {
	display: block;
}
h1 { font-family: 'Telenor', sans-serif; }
</style>
